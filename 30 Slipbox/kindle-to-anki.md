---
modified: 2025-02-19T06:44:17-05:00
---

Kindle to Anki script
tags:: #books 
up:: [[Kindle]]
```
import os
import csv
from bs4 import BeautifulSoup

# Define the path to the Downloads folder
downloads_folder = os.path.expanduser('~/Downloads')

# Prepare the CSV file
csv_filename = 'anki_deck.csv'
with open(csv_filename, 'w', newline='', encoding='utf-8') as csvfile:
    fieldnames = ['Highlight', 'Note', 'Title', 'Location', 'Page', 'Chapter']
    writer = csv.DictWriter(csvfile, fieldnames=fieldnames, delimiter=':')
    # writer.writeheader()

    # Loop through all HTML files in the Downloads folder
    for filename in os.listdir(downloads_folder):
        if filename.endswith('.html'):
            file_path = os.path.join(downloads_folder, filename)

            # Read and parse the HTML file
            with open(file_path, 'r', encoding='utf-8') as file:
                soup = BeautifulSoup(file, 'html.parser')

                # Extract the book title
                book_title = soup.find('div', class_='bookTitle').get_text(strip=True) if soup.find('div', class_='bookTitle') else ''

                # Initialize variables
                section_heading = None

                # Iterate over the HTML elements
                for element in soup.find_all(['div']):
                    if 'sectionHeading' in element.get('class', []):
                        section_heading = element.get_text(strip=True)
                    elif 'noteHeading' in element.get('class', []):
                        note_heading = element.get_text(strip=True)
                        page_location = note_heading.split(' - ')[1]
                        page = page_location.split(' · ')[0].replace('Page ', '') if 'Page ' in page_location else ''
                        location = page_location.split(' · ')[1].replace('Location ', '') if 'Location ' in page_location else ''
                    elif 'noteText' in element.get('class', []):
                        note_text = element.get_text(strip=True)
                        # Determine if it's a highlight or a note
                        if 'Highlight' in note_heading:
                            highlight = note_text
                            note = ''
                        else:
                            highlight = 'Note-Only'
                            note = note_text
                        writer.writerow({
                            'Highlight': highlight,
                            'Note': note,
                            'Title': book_title,
                            'Location': location,
                            'Page': page,
                            'Chapter': section_heading
                        })

print(f"CSV file '{csv_filename}' created successfully.")

```