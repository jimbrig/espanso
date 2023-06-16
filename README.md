# Espanso <img align="right" syle='float' href='https://user-images.githubusercontent.com/32652297/139356362-d02ef475-1b0e-4b73-9d9c-7b7e147cb426.png' src='https://user-images.githubusercontent.com/32652297/139356362-d02ef475-1b0e-4b73-9d9c-7b7e147cb426.png' />

> **Note**: 
> *My personal [Espanso](https://espanso.org/) text expander configuration files and setup.*

*This repository is a part of my [dotfiles]().*

***

<center>


<!--Start:Badges-->
[![Generate Changelog](https://github.com/jimbrig/espanso/actions/workflows/changelog.yml/badge.svg)](https://github.com/jimbrig/espanso/actions/workflows/changelog.yml)
<!--End:Badges-->

[Espanso Website](https://espanso.org/) | [EspansoHub](https://hub.espanso.org/) | [Documentation](https://espanso.org/docs/get-started/) | [Reddit Community](https://www.reddit.com/r/espanso/) | [GitHub](https://github.com/federico-terzi/espanso)

</center>

***

## Contents

<!-- TOC -->

- [Contents](#contents)
- [What is espanso?](#what-is-espanso)
    - [What is a Text Expander?](#what-is-a-text-expander)
    - [Key Features](#key-features)
- [Setup](#setup)
    - [Installation](#installation)
    - [Configuration](#configuration)
    - [Notes](#notes)
- [User Scripts](#user-scripts)
- [Editing](#editing)
- [Toggle](#toggle)
- [Application Specific](#application-specific)

<!-- /TOC -->


## What is `espanso`?

[Espanso](https://espanso.org/) is an Open Source, Cross-Platform Text Expander tool written in Rust.

### What is a Text Expander?

A *text expander* is a program that detects when you type a specific **keyword** and replaces it with **something else**.

This is useful in many ways, including but not limited to:

- **Save a lot of typing**, expanding common sentences.
- Create **system-wide** code snippets.
- Execute **custom scripts**
- Use **emojis** like a pro.

### Key Features

* Works on **Windows**, **macOS** and **Linux**
* Works with almost **any program**
* Works with **Emojis** 😄
* Works with **Images**
* Includes a powerful **Search Bar** 🔎
* **Date** expansion support
* **Custom scripts** support
* **Shell commands** support
* **App-specific** configurations
* Support [Forms](https://espanso.org/docs/matches/forms/)
* Expandable with **packages**
* Built-in **package manager** for [espanso hub](https://hub.espanso.org/)
* File based configuration
* Support Regex triggers
* Experimental Wayland support

## Setup

### Installation

Install via on Windows using a package manager of choice:

- `winget`
- `chocolatey`
- `scoop`

```powershell
# winget
winget install FedericoTerzi.espanso

# chocolatey
sudo cinst -y espanso

# scoop
scoop install espanso
```

`espanso` should launch at startup, but to check run `espanso status`, and if it says *`espanso is not running`* then run *`espanso start`*.

### Configuration

`espanso` uses a file-based configuration approach. Simply run `espanso path` to determine the configuration folder's path.

```powershell
> ~\AppData\Roaming\espanso :: git(main) 10:43:57
➜ wsl -e tree
.
├── README.md
├── default.yml
└── user
    ├── credit-cards.yml
    ├── dev-secrets.yml
    ├── dev.yml
    ├── emails.yml
    ├── links.yml
    ├── passwords.yml
    ├── phone-numbers.yml
    └── websites.yml

1 directory, 10 files
```

### Notes

`espanso` scripts should be located at `%APPDATA%\espanso` (on Windows) [^1] with a file named `default.yml` and (optionally) a sub-directory named `user`
(i.e. `%APPDATA%\espanso\user`).

Place sub-level child-scripts in the user folder.

## User Scripts

Currently I have a total of 8 user-specific child scripts under parent *default.yml*, which are housed in the [user dirctory](user/):

- [credit-cards.yml](user/credit-cards.yml): My credit cards [^2]
- [dev-secrets.yml](user/dev-secrets.yml): Developer secrets [^2]
- [dev.yml](user/dev.yml): Development related replacements (i.e. common code strings).
- [emails.yml](user/emails.yml): My email addresses
- [links.yml](user/links.yml): Personal websites
- [passwords.yml](user/passwords.yml): My common passwords [^2]
- [phone-numbers.yml](user/phone-numbers.yml): My cell phone numbers
- [websites.yml](user/websites.yml): Similar to `links.yml`

## Editing

For quick editing of espanso scripts run `espanso edit`.

## Toggle

To toggle `espanso`'s runtime simply double-tab the `Alt` key. This makes it useful to temporarilly disable then re-enable the service.

## Application Specific

Use the `filter_title` configuration variable to specify expansions that should only apply in windows with a title of the provided value. For example, to only match and trigger the below expansion in Outlook you would use:

```yaml
filter_title: "Outlook"
matches:
    - trigger: ":signature"
      replace: "Jimmy Briggs"
```

The following table lays out all possible `filter_*` configurations:

| Filter         | Description                                             | Windows Support                              | MacOS Support                                       | Linux Support   |
| -------------- | ------------------------------------------------------- | -------------------------------------------- | --------------------------------------------------- | --------------- |
| `filter_title` | Filter based on the current Window title                | Full support                                 | Uses the App identifier instead of the Window title | Full support    |
| `filter_exec`  | Filter based on the current application executable path | Full support                                 | Full support                                        | Partial support |
| `filter_class` | Filter based on the current Window class                | Uses the application executable path instead | Uses the App identifier instead                     | Full support    |

***

[^1]: File Paths are Operating Sysstem Dependent:
    - Linux: `$XDG_CONFIG_HOME/espanso` (e.g. `/home/user/.config/espanso`)
    - macOS: `$HOME/Library/Preferences/espanso` (e.g. `/Users/user/Library/Preferences/espanso`)
    - Windows: `{FOLDERID_RoamingAppData}\espanso` (e.g. `%APPDATA%\espanso)`)


[^2]: Encrypted via [git-crypt]().
