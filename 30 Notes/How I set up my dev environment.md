---
created: 2024-04-27 16:18
modified: 2025-06-16T07:05:44-04:00
---
up::  [[tools]]
## How I set up my dev environment

**Table of Contents**
- [[#How I set up my dev environment|How I set up my dev environment]]
- [[#OS Settings|OS Settings]]
	- [[#OS Settings#Desktop|Desktop]]
	- [[#OS Settings#Finder|Finder]]
	- [[#OS Settings#Dock|Dock]]
- [[#Homebrew|Homebrew]]
	- [[#Homebrew#Install Apps|Install Apps]]
	- [[#Homebrew#iTerm2|iTerm2]]
- [[#Shell|Shell]]
		- [[#iTerm2#Load dotfiles|Load dotfiles]]
	- [[#Shell#Github SSH Setup|Github SSH Setup]]
- [[#Node.js|Node.js]]

## OS Settings
These are my preferred settings for `Desktop`, `Finder` and the `Dock`.
### Desktop
I don't like the new Desktop, Stage Manager or Widget features in Sonoma, so I disable them.

- System Preferences
    - Desktop & Dock
        - Desktop & Stage Manager
            - Show Items
                - On Desktop -> uncheck
                - In Stage Manager -> uncheck
            - Click wallpaper to reveal desktop -> Only in Stage Manager
            - Stage Manager -> uncheck
            - Widgets
                - On Desktop -> uncheck
                - In Stage Manager -> uncheck

### Finder
- Finder -> Preferences
    - General -> Show these on the desktop -> Select None
        - I try to keep my desktop completely clean.
    - General -> New Finder windows show -> Home Folder
        - I prefer to see my home folder in each new finder window instead of recent documents
    - Advanced -> Show all filename extensions -> Yes
    - Advanced -> Show warning before changing an extension -> No
    - Advanced -> When performing a search -> Search the current folder
- View
    - Show Status Bar
    - Show Path Bar
    - Show Tab Bar

### Dock
I don't use the Dock at all. It takes up screen space, and I can use RayCast to launch apps and AltTab to switch between apps. I make the dock as small as possible and auto hide it.

- System Preferences
    - Desktop & Dock
        - Size -> Small as possible
        - Position on screen -> Left
        - Automatically hide and show the Dock -> Yes
        - Animate opening applications -> No
        - Show suggested and recent apps in the Dock -> No


## Homebrew
[Homebrew](https://brew.sh/) allows us to install tools and apps from the command line.

To install it, open up the built in `Terminal` app and run this command:

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

This will also install the xcode build tools which is needed by many other developer tools.

After Homebrew is done installing, we will use it (via RayCast) to install everything else we need.

Install raycast using homebrew
```
brew install raycast
```

Install the [RayCast Homebrew Plugin](https://www.raycast.com/nhojb/brew) so we can easily install formulae and casks directly from RayCast.
Install Raycast Bitwarden Plugin

### Install Apps

```
rectangle
hiddenbar
git
zsh
```

```
xargs brew install < tools.txt
```

```
visual-studio-code
selfcontrol
ticktick
notion
obsidian
arc
spark
iterm2
docker
google-drive
```

```
xargs brew install --cask < apps.txt
```
**install thinkbuddy**

### iTerm2

Once installed, launch it and customize the settings / preferences to your liking. These are my preferred settings:
- Appearance
    - Theme
        - Minimal
- Profiles
    - Default
        - General -> Working Directory -> Reuse previous session's directory
        - Colors -> Basic Colors -> Foreground -> Lime Green
        - Text -> Font -> Anonymous Pro
            - You can download this font [here](https://www.marksimonson.com/fonts/view/anonymous-pro).
            - I use this font in VS Code as well
        - Text -> Font Size -> 36
            - I use my Macbook to present / teach, so a big font size is important so everyone can see the commands I'm typing
        - Keys -> Key Mappings -> Presets -> Natural Text Editing
            - This allows me to use the [keyboard shortcuts](https://gist.github.com/w3cj/022081eda22081b82c52) I know and love inside of iTerm2



## Shell
Mac now comes with `zsh` as the default [shell](https://en.wikipedia.org/wiki/Comparison_of_command_shells). I've switched to using this with [Oh My Zsh](https://ohmyz.sh/).

#### Load dotfiles
All my dotfiles are stored on [dotfiles](https://github.com/VivianLin61/dotfiles/tree/main/dotfiles)
I clone this repo to my machine and copy the files into my home directory.

### Github SSH Setup
- Follow [this guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) to setup an ssh key for github
- Follow [this guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) to add the ssh key to your github account

## Node.js
I use nvm to manage the installed versions of Node.js on my machine. This allows me to easily switch between Node.js versions depending on the project I'm working in.

See installation instructions [here](https://github.com/nvm-sh/nvm#installing-and-updating).

OR run this command (make sure v0.39.7 is still the latest)

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

Now that nvm is installed, you can install a specific version of node.js and use it:

```shell
nvm install 20
nvm use 20
node --version
```

[Installation | pnpm](https://pnpm.io/installation)
```
curl -fsSL https://get.pnpm.io/install.sh | sh -
```

### Vscode
1. Install project manager
	2. Select repo to read project files from
**Resources**
[GitHub - CodingGarden/mac-setup: This repo contains info on all the apps / tools / settings I use on my Mac.](https://github.com/CodingGarden/mac-setup)


**Linked References to this Note**
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```



