```
import os
import regex
import zipfile
from bs4 import BeautifulSoup
from lxml import etree
from tqdm import tqdm
import warnings
import stkclient
from pathlib import Path

with open('client.json', 'r') as f:
    client = stkclient.Client.load(f)

warnings.filterwarnings("ignore", category=UserWarning, module='bs4')

def bionic_word(word):
    if len(word) <= 1:
        return word
    elif len(word) <= 3:
        return f"<b>{word[:1]}</b>{word[1:]}"
    else:
        midpoint = len(word) // 2
        return f"<b>{word[:midpoint]}</b>{word[midpoint:]}"

def process_text(text):
    word_pattern = regex.compile(r'\b[\p{L}\p{M}]+\b', regex.UNICODE)

    def replace_word(match):
        word = match.group(0)
        return bionic_word(word)

    return word_pattern.sub(replace_word, text)

def process_html_content(content):
    soup = BeautifulSoup(content, 'lxml')

    skip_tags = {'script', 'style', 'pre', 'code'}

    for element in soup.find_all(text=True):
        if element.parent.name not in skip_tags:
            new_text = process_text(element.string)
            new_element = BeautifulSoup(new_text, 'html.parser')
            element.replace_with(new_element)

    return str(soup)

def process_epub(input_path, output_path):
    with zipfile.ZipFile(input_path, 'r') as zip_ref:
        file_list = zip_ref.infolist()
        total_files = len(file_list)

        with zipfile.ZipFile(output_path, 'w') as zip_out:
            with tqdm(total=total_files, desc="Processing files", unit="file") as pbar:
                for file_info in file_list:
                    with zip_ref.open(file_info) as file:
                        content = file.read()

                        if file_info.filename.endswith(('.html', '.xhtml', '.htm')):
                            content = process_html_content(content)
                        elif file_info.filename.endswith('content.opf'):
                            # Do not modify content.opf
                            pass

                        zip_out.writestr(file_info, content)

                    pbar.update(1)
                    pbar.set_postfix(current_file=file_info.filename)

def main():
    # Set input_dir to the Downloads folder
    input_dir = os.path.expanduser('~/Downloads')
    output_dir = 'outputs'

    # Ensure the output directory exists
    os.makedirs(output_dir, exist_ok=True)

    # Process each EPUB file in the input directory
    for filename in os.listdir(input_dir):
        if filename.endswith('.epub'):
            # Remove '(Z-Library)' from the filename
            clean_filename = filename.replace(' (Z-Library)', '')

            input_path = os.path.join(input_dir, filename)
            output_path = os.path.join(output_dir, clean_filename)


            print(f"Processing '{filename}'...")
            try:
                process_epub(input_path, output_path)
                # Create a Path object
                path_obj = Path(output_path)
                # destinations = [d.device_serial_number for d in devices.owned_devices]
                client.send_file(path_obj, ["08C185BFB09340EC8C022D18D9659F19"], author="", title=filename, format="epub")
                print(f"Conversion complete. Output saved to '{output_path}'")
            except Exception as e:
                print(f"Error occurred during processing '{filename}': {str(e)}")


    # Clean up the input and output directories, removing only .epub files
    for directory in [input_dir, output_dir]:
        for file in os.listdir(directory):
            file_path = os.path.join(directory, file)
            try:
                if file.endswith('.epub') and (os.path.isfile(file_path) or os.path.islink(file_path)):
                    os.unlink(file_path)  # Remove the .epub file or link
            except Exception as e:
                print(f"Failed to delete {file_path}. Reason: {e}")

if __name__ == "__main__":
    main()

```