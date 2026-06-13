<div align="center">

# 📚 lib-x

```text
██╗░░░░░██╗██████╗░░░░░░░██╗░░██╗
██║░░░░░██║██╔══██╗░░░░░░╚██╗██╔╝
██║░░░░░██║██████╦╝█████╗░╚███╔╝░
██║░░░░░██║██╔══██╗╚════╝░██╔██╗░
███████╗██║██████╦╝░░░░░░██╔╝╚██╗
╚══════╝╚═╝╚═════╝░░░░░░░╚═╝░░╚═╝
```

**Browse and manage your Calibre library from the terminal**

![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![macOS](https://img.shields.io/badge/macOS-000000?style=flat-square&logo=apple&logoColor=white)
![Windows](https://img.shields.io/badge/Windows-0078D6?style=flat-square&logo=windows&logoColor=white)
![Android](https://img.shields.io/badge/Android-3DDC84?style=flat-square&logo=android&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)
![Core](https://img.shields.io/badge/Core-Calibre%20%7C%20FZF%20%7C%20JQ-blue?style=flat-square)

<details>
<summary>Click to view screenshots</summary>
<br>

_(Add your screenshots here!)_

<!-- <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/your-image-hash" /> -->

</details>

## Table of Contents

- [Features](#features)
- [Installation](#installation)
  - [Prerequisites](#prerequisites)
  - [Universal Installation](#universal-installation)
  - [Platform-Specific Instructions](#platform-specific-instructions)
- [Usage](#usage)
  - [Quick Start](#quick-start)
  - [Command-Line Options](#command-line-options)
  - [Environment Variables](#environment-variables)
  - [Examples & Workflows](#examples--workflows)
- [Configuration](#configuration)
  - [Configuration File Location](#configuration-file-location)
  - [Configuration Variables](#configuration-variables)
- [Extensions](#extensions)
  - [Official Extensions](#official-extensions)
- [Frequently Asked Questions (FAQ)](#frequently-asked-questions-faq)
- [Contribution](#contribution)
- [Support](#support)

## Features

- **Multiple Launcher Support**: Browse your library with `fzf`, `rofi`, or `gum`, all supporting high-quality cover previews.
- **Calibre Integration**: Seamlessly interfaces with `calibredb` to fetch, search, sort, add, and remove books without ever touching the bloated Calibre GUI.
- **Smart Caching**: `lib-x` caches your entire library to a local JSON file on startup. It only updates when it detects file changes, making browsing massive libraries instantaneous.
- **Custom User Lists**: Manage your reading habits with built-in states: Reading List, Paused, Re-reading, Planning, Completed, Dropped, and Docs.
- **Metadata Editing**: Quickly edit titles, authors, tags, rating, and publishers directly from the terminal.
- **Cover Previews**: View beautiful book covers directly in your terminal using `icat`, `chafa`, or `imgcat`.
- **Search & Sort**: Utilize native Calibre search syntax to filter books, and sort them dynamically by size, author, date, etc.
- **File Explorer Support**: Use `yazi` or `fzf` to navigate your local filesystem and easily add single books or entire directories to your Calibre library.
- **Background Reading**: Option to disown the reading process (`CONFIG_DISOWN_READING_PROCESS`), allowing you to close `lib-x` while keeping your eBook reader open.
- **Theming & Styling**: Native theming support through `.theme` extensions, with Tokyo Night set as the default.
- **Multi-language Support**: Loadable language files (`.lang`) to easily localize UI prompts and messages.
- **Scriptable Shortcuts**: Bypass menus and jump straight to specific lists, searches, or actions using direct command-line flags.
- **Desktop Integration**: Generate a `.desktop` file to be launched natively from application menus (Linux) combined perfectly with Rofi.
- **Auto-Updater**: Built-in update checker that securely pulls the latest version from GitHub and allows you to apply the update in-place.
- **Shell Completions**: Includes shell completions (Fish currently supported) to tab-complete searches, config options, and specific menus.

## Installation

![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![macOS](https://img.shields.io/badge/macOS-000000?style=flat-square&logo=apple&logoColor=white)
![Windows](https://img.shields.io/badge/Windows-0078D6?style=flat-square&logo=windows&logoColor=white)
![Arch Linux](https://img.shields.io/badge/Arch_Linux-1793D1?style=flat-square&logo=arch-linux&logoColor=white)

### Prerequisites

**Required:**

- `calibre` - For providing the `calibredb` CLI tool.
- `fzf` - Main launcher.
- `jq` - For parsing the library cache JSON.
- `curl` - For fetching script updates and installers.
- `sh` - Any POSIX-compliant shell.
- **Nerd Font** - For the icons (Recommended JetBrains Mono Nerd Font).

**Optional:**

- **Terminal Image Viewers:**
  - `icat` _(Recommended for Kitty and Ghostty)_
  - `chafa` _(Cross-terminal)_
  - `imgcat` _(For iTerm2/WezTerm)_
- **File Explorers:** `yazi` _(Highly recommended for adding books)_
- **Alternate Launcher:** `rofi` _(Great if you want a desktop app launcher)_
- **Terminal QoL:** `gum` _(Better terminal UI; loaders, prompts etc)._

---

### Universal Installation

Ensure `~/.local/bin` exists and is added to your system's `$PATH`.

```bash
# Automated interactive installer
# Helps you setup dependencies and configure themes, languages, and other options.
curl -sL "https://raw.githubusercontent.com/Benexl/lib-x/refs/heads/master/installer" | sh

# Or manual setup
curl -sL "https://github.com/Benexl/lib-x/releases/download/v0.2.0/lib-x" -o ~/.local/bin/lib-x
chmod +x ~/.local/bin/lib-x
```

_To uninstall, just run: `rm ~/.local/bin/lib-x`_, then to remove its related data folders `rm -rf ~/.config/lib-x` and `rm -rf ~/.cache/lib-x`.

---

### Platform-Specific Instructions

<details>
<summary><b>Arch Linux (AUR)</b></summary>

```bash
yay -S lib-x-git

# or if you prefer paru

paru -S lib-x-git
```

</details>

## Usage

You can opt to use it interactively via menus or via cmdline shortcuts for purposes of scripting or keybinding.

```bash
lib-x [OPTIONS]
lib-x completions [--fish | --bash | --zsh | --help]
```

### Quick Start

To launch the interactive terminal interface with your default settings, run:

```bash
lib-x
```

---

### Command‑Line Options

#### Search & Sort

- `-s, --search <term>` : Search for a book based on Calibre's native search syntax.
- `-S, --sort-by <field>` : Sort the library based on a specific field (e.g., `author_sort`, `size`, `timestamp`).

#### Access Lists & Categories

You can jump straight into a list or category and skip the main menu:

- `-g, --go-directly-to <menu>` : Open a specific sub-menu natively (e.g., `Authors`, `Tags`).
- `--reading-list` : Open your Reading List directly.
- `--recent` : Open your Recent books directly.
- `--paused` : Open your Paused list directly.
- `--rereading` : Open your Re-reading list directly.
- `--planing` : Open your Planning list directly.
- `--completed` : Open your Completed list directly.
- `--docs` : Open your Docs list directly.
- `--dropped` : Open your Dropped list directly.
- `--all` : Browse all books in your library.
- `--random` : Browse random books directly.
- `--misc, --miscellaneous` : Open the Miscellaneous menu.

#### UI & Rofi Settings

- `-l, -p, --preferred-selector <fzf|rofi|gum>` : Override the default menu launcher.
- `--preview` : Enable the preview window _(covers/metadata)_
- `--no-preview` Disable the preview window
- `--rofi-theme-main <path>` : Override the Rofi main theme.
- `--rofi-theme-preview <path>` : Override the Rofi preview theme.

#### Book Action Shortcuts

All these options can be paired with `--book-exit` (`-be`) to terminate the CLI immediately after the action completes.

- `--read` : Read the selected book.
- `--edit-metadata` : Open the metadata editor for the selected book.
- `--remove-book` : Remove the selected book from the library.
- `-bs, --book-skip` : Skip the book selection menu and automatically pick the first entry.
- `-be, --book-exit` : Exit after performing a book action.

#### Others

- `-x, --extension <ext>` : Load a specific extension file _(supports fish tab complete)_.
- `-e, --edit-config` : Open the `lib-x` configuration file in your `$EDITOR`.
- `-U, --update` : Check for and apply the latest script update from GitHub.
- `-E, --generate-desktop-entry` : Print a `.desktop` application entry to `stdout`; perfectly paired with Rofi.
- `-d, --disown-reading-process` : Detach the reading process from the terminal.
- `-D, --no-disown-reading-process` : Keep the reading process attached to the terminal.
- `-r, --no-of-random-books <num>` : Set the number of random books to show.
- `--private` : Do not update the recent history list during this session.
- `--config-write` : Write the current runtime config to the config file.

---

### Environment Variables

Almost all CLI options can be permanently set in `~/.config/lib-x/lib-x.conf` or overridden using environment variables.

- `LIB_X_LAUNCHER` (e.g., `fzf` or `rofi`)
- `LIB_X_CALIBRE_LIBRARY_PATH` (e.g., `~/Books`)
- `LIB_X_ENABLE_PREVIEW` (`true` or `false`)
- `LIB_X_IMAGE_RENDERER` (`chafa`, `icat`, `imgcat`)
- `LIB_X_FILE_EXPLORER` (`yazi`, `fzf`)

---

### Examples & Workflows

**Hello world**

```bash
# Save your current runtime settings to the config file
LIB_X_IMAGE_RENDERER=icat LIB_X_LAUNCHER=fzf lib-x --preview --config-write
```

**Desktop app launcher**
Launch `lib-x` as a graphical application using Rofi.

```bash
lib-x --preferred-selector rofi --preview --disown-reading-process
```

**Quick Search & Read**

```bash
# Search for chess books, sort by size, skip the selection menu, open the book, and exit the CLI
lib-x --search "tag:chess" --sort-by "size" --book-skip --read --book-exit
```

**Jump straight to your Reading List**

```bash
lib-x --reading-list
```

**Generate a Desktop Entry**

```bash
lib-x -E > ~/.local/share/applications/lib-x.desktop
```

**Shell Completions**

```bash
# Fish shell completions
lib-x completions --fish > ~/.config/fish/completions/lib-x.fish
```

## Configuration

By default, the main configuration file is located at:

```bash
~/.config/lib-x/lib-x.conf
```

_(Note: It respects the `$XDG_CONFIG_HOME` environment variable if set)._

You can open it using the cli:

```bash
lib-x --edit-config
```

---

### Configuration Variables

#### Display & Interface

| Variable                       | Default             | Description                                                            |
| :----------------------------- | :------------------ | :--------------------------------------------------------------------- |
| `CONFIG_LAUNCHER`              | `fzf`               | The menu launcher tool to use. Options: `fzf`, `rofi`, `gum`.          |
| `CONFIG_ENABLE_COLORS`         | `true`              | Enable or disable ANSI true-color formatting in the UI.                |
| `CONFIG_EDITOR`                | `vi` (or `$EDITOR`) | Text editor used for editing configs and files.                        |
| `CONFIG_NOTIFICATION_DURATION` | `5`                 | Duration (in seconds) for desktop/CLI notifications to remain visible. |

#### Media & Covers

| Variable                       | Default | Description                                                                     |
| :----------------------------- | :------ | :------------------------------------------------------------------------------ |
| `CONFIG_ENABLE_PREVIEW`        | `false` | Enable or disable the preview window (metadata & descriptions).                 |
| `CONFIG_ENABLE_PREVIEW_IMAGES` | `false` | Whether to render book covers in the preview window.                            |
| `CONFIG_IMAGE_RENDERER`        | `chafa` | Tool used to render images in the terminal. Options: `chafa`, `icat`, `imgcat`. |

#### Calibre Handling

| Variable                        | Default             | Description                                                     |
| :------------------------------ | :------------------ | :-------------------------------------------------------------- |
| `CONFIG_CALIBRE_LIBRARY_PATH`   | `~/Calibre Library` | Absolute path to your active Calibre library folder.            |
| `CONFIG_FILE_EXPLORER`          | `yazi` (or `fzf`)   | Tool used when selecting "Add Books From Folder".               |
| `CONFIG_DISOWN_READING_PROCESS` | `true`              | Run the eBook reader in the background without blocking the UI. |

#### History & Lists

| Variable                    | Default | Description                                                         |
| :-------------------------- | :------ | :------------------------------------------------------------------ |
| `CONFIG_UPDATE_RECENT`      | `true`  | Save books automatically to the Recent list when you select "Read". |
| `CONFIG_NO_OF_RECENT`       | `30`    | The maximum number of books to retain in your Recent list.          |
| `CONFIG_NO_OF_RANDOM_BOOKS` | `30`    | Number of books to fetch when generating a Random list.             |

#### Fzf and Rofi

| Variable                    | Default        | Description                                                                            |
| :-------------------------- | :------------- | :------------------------------------------------------------------------------------- |
| `CONFIG_FZF_OPTS`           | _(see config)_ | Fine‑tune `fzf` layout, colors, pointers, and keybindings. Defaults to "Tokyo Night" . |
| `CONFIG_ROFI_THEME_MAIN`    | `""`           | Path to a custom Rofi `.rasi` theme for the main menu.                                 |
| `CONFIG_ROFI_THEME_PREVIEW` | `""`           | Path to a custom Rofi `.rasi` theme for the preview menu.                              |

## Extensions

`lib-x` supports **extensions** to add or override functionality without modifying the core script.  
Extensions are shell scripts placed in `~/.config/lib-x/extensions/` and can be loaded on demand or automatically.

### Official Extensions

The following extensions are maintained and included in the repository.

#### Language Extensions (`langs/`)

<details>
<summary><code>es.lang</code></summary>

Spanish translation for all UI texts, prompts, and messages.

**Load with:**  
`lib-x -x langs/es.lang`

</details>

#### Theme Extensions (`themes/`)

<details>
<summary><code>catppuccin-mocha.theme</code></summary>

Applies the **Catppuccin Mocha** color scheme to `fzf` and the terminal output.

**Load with:**  
`lib-x -x themes/catppuccin-mocha.theme`

</details>

### Loading Extensions

**Temporary (single session)**

```bash
lib-x -x langs/es.lang
lib-x -x themes/catppuccin-mocha.theme
```

**Permanent**  
Add to `~/.config/lib-x/lib-x.conf`:

```bash
CONFIG_AUTOLOADED_EXTENSIONS="themes/catppuccin-mocha.theme,langs/es.lang"
```

## Frequently Asked Questions (FAQ)

<details>
<summary><b>Reporting Bugs</b></summary>
<br>

`lib-x` is a wrapper over `calibredb`. Before opening an issue, please determine if the bug is related to `calibredb` itself.

- **Database lock errors or missing books:** Handled by Calibre. Make sure the Calibre GUI is closed, or use a networked Calibre server setup.
- **UI logic, states, or previews fail:** This is handled by `lib-x`. Please open an issue!

</details>

<details>
<summary><b>Why is my library empty or not updating?</b></summary>
<br>

`lib-x` caches your library into `~/.cache/lib-x/calibre_db.json`. It looks at the Last Modified timestamp of your `CONFIG_CALIBRE_LIBRARY_PATH` to know when to refresh.
If books aren't showing up, select **Miscellaneous -> Reload Data** in the menu to force a cache refresh.

</details>

<details>
<summary><b>How does lib-x open books? Can I change my reader?</b></summary>
<br>

`lib-x` uses your operating system's native file opener (`open` on macOS, `xdg-open` on Linux, `cmd.exe` on Windows/WSL).
To change your eBook reader, you must change your system's default MIME type association for `.epub`, `.pdf`, etc.
For example, on Linux:
`xdg-mime default org.pwmt.zathura.desktop application/epub+zip`

</details>

<details>
<summary><b>Why are my image previews not showing up?</b></summary>
<br>

Image previews require a few components to work together:

1. Ensure you have enabled them in your config: `CONFIG_ENABLE_PREVIEW=true` and `CONFIG_ENABLE_PREVIEW_IMAGES=true`.
2. Ensure you have a supported image renderer installed (e.g., `chafa`, `icat`, or `imgcat`).
3. Set the correct renderer in your config: `CONFIG_IMAGE_RENDERER="chafa"`.
4. Ensure your terminal emulator actually supports image rendering. If it doesn't, stick with `chafa`, which falls back to excellent ASCII/block character rendering.

</details>

<details>
<summary><b>Previews overlap text or look distorted. How do I fix this?</b></summary>
<br>

If your images are overlapping with UI text, your terminal may not properly support the image clearing sequences used by `chafa`.

1. **Kitty / Ghostty:** Set `CONFIG_IMAGE_RENDERER="icat"`.
2. **iTerm2 / WezTerm:** Try `CONFIG_IMAGE_RENDERER="imgcat"`.
3. **Other Terminals:** Stick to `CONFIG_IMAGE_RENDERER="chafa"`, but ensure your terminal supports Sixel.

</details>

## Contribution

Pull requests are highly welcome :)

### Supporting the Project

If you enjoy using `lib-x` and want to support its ongoing development, **consider leaving a Star on GitHub!**
