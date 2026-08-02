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
![License](https://img.shields.io/badge/License-GPL_v3-yellow?style=flat-square)
![Core](https://img.shields.io/badge/Core-Calibre%20%7C%20FZF%20%7C%20JQ-blue?style=flat-square)
</div>

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
- **Calibre Integration**: Seamlessly interfaces with `calibredb` to fetch, search, sort, add, and remove books without ever touching the bloated Calibre GUI. Includes capabilities to `convert`, `polish`, and launch the `ebook-viewer`.
- **Smart Caching**: `lib-x` caches your entire library to a local JSON file on startup. It only updates when it detects file changes, making browsing massive libraries instantaneous. Caches automatically clean up after 7 days.
- **Interactive Shell Mode**: Spawn an interactive shell populated with exported environment variables for the selected book(s) allowing manual command-line execution.
- **Custom User Lists**: Manage your reading habits with built-in states: Reading, Paused, Re-reading, Planning, Completed, Dropped, and Docs. Includes a history of Recent books.
- **Metadata Editing**: Quickly edit titles, authors, tags, ratings, and publishers directly from the terminal.
- **Cover Previews**: View beautiful book covers directly in your terminal using `icat`, `chafa`, or `imgcat`.
- **Search & Sort**: Utilize native Calibre search syntax to filter books, and sort them dynamically by size, author, date, ratings, identifier, etc. Saves local search history.
- **File Explorer Support**: Use `yazi` or `fzf` to navigate your local filesystem and easily add single books or entire directories to your Calibre library.
- **Background Reading**: Option to disown the reading process (`CONFIG_READING_PROCESS_DISOWN`), allowing you to close `lib-x` while keeping your eBook reader open. Define explicit readers using `CONFIG_READER` (e.g., `pdf:zathura,epub:foliate`).
- **Theming & Styling**: Native theming support through `.theme` extensions, with Tokyo Night set as the default.
- **Multi-language Support**: Loadable language files (`.lang`) to easily localize UI prompts and messages.
- **Scriptable Shortcuts**: Bypass menus and jump straight to specific lists, searches, or actions using direct command-line flags.
- **Desktop Integration**: Generate a `.desktop` file to be launched natively from application menus (Linux) combined perfectly with Rofi.
- **Auto-Updater**: Built-in update checker that securely pulls the latest version from GitHub and allows you to apply the update in-place, showing code diffs.
- **Shell Completions**: Includes shell completions for `fish`, `bash`, and `zsh`.

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
- **E-Book Utilities**: `ebook-viewer`, `ebook-convert`, `ebook-edit`, `ebook-polish`, `ebook-meta` (usually bundled with Calibre).

---

### Universal Installation

Ensure `~/.local/bin` exists and is added to your system's `$PATH`.

```bash
# Automated interactive installer
# Helps you setup dependencies and configure themes, languages, and other options.
curl -sL "https://raw.githubusercontent.com/Benexl/lib-x/refs/heads/master/installer" | sh

# Or manual setup
curl -sL "https://github.com/Benexl/lib-x/releases/download/v0.5.0/lib-x" -o ~/.local/bin/lib-x
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

#### Core Flags
- `-h, --help` : Show the help message and exit.
- `-v, --version` : Print version information and exit.
- `-e, --edit-config` : Open the `lib-x` configuration file in your `$EDITOR`.
- `-U, --update` : Check for and apply the latest script update from GitHub.
- `-E, --generate-desktop-entry` : Print a `.desktop` application entry to `stdout`; perfectly paired with Rofi.
- `--config-write` : Write the current runtime config to the config file.

#### Search & Sort
- `-s, --search [term]` : Search for a book. If no term is provided, it prompts you interactively.
- `-S, --sort-by [field]` : Sort the library based on a field (e.g., `author_sort`, `size`, `timestamp`, `pubdate`, `rating`). Append `_asc` for ascending. If no field is provided, it prompts you interactively.

#### Access Lists & Categories
You can jump straight into a list or category and skip the main menu:

- `--reading-list` : Open your Reading List directly.
- `--recent` : Open your Recent books directly.
- `--paused` : Open your Paused list directly.
- `--rereading` : Open your Re-reading list directly.
- `--planning` : Open your Planning list directly.
- `--completed` : Open your Completed list directly.
- `--docs` : Open your Docs list directly.
- `--dropped` : Open your Dropped list directly.
- `--all` : Browse all books in your library.
- `-r, --no-of-random-books [num]` : Set the number of random books to show (opens Random menu).
- `--random` : Browse random books directly.
- `--misc, --miscellaneous` : Open the Miscellaneous menu.

#### UI & Display Settings
- `-l, --launcher <fzf|rofi|gum>` : Override the default menu launcher.
- `--preview` : Enable the preview window (metadata & descriptions).
- `--no-preview` : Disable the preview window.
- `--preview-images` : Enable image covers in the preview window.
- `--no-preview-images` : Disable image covers in the preview window.
- `--rofi-theme-main <path>` : Override the Rofi main theme.
- `--rofi-theme-preview <path>` : Override the Rofi preview theme.
- `--rofi-theme-prompt <path>` : Override the Rofi prompt theme.
- `--rofi-theme-confirm <path>` : Override the Rofi confirm theme.

#### Book Action Shortcuts
All these options can be paired with `--book-exit` (`-be`) to terminate the CLI immediately after the action completes, or `--cmd-exit` (`-ce`) to exit after menu processes.

- `--read` : Read the selected book.
- `--edit-metadata` : Open the metadata editor for the selected book.
- `--remove-book` : Remove the selected book from the library.
- `--viewer` : Open the selected book in the Calibre ebook-viewer.
- `--convert` : Convert the selected book to another format.
- `--edit-book` : Open the selected book in Calibre ebook-edit.
- `--polish` : Polish the selected book.
- `--show-metadata` : Display metadata using ebook-meta.
- `-bs, --book-skip` : Skip the book selection menu and automatically pick the first entry.
- `-be, --book-exit` : Exit after performing a book action.
- `-ce, --cmd-exit` : Exit after shortcut menu commands.

#### Extensions & Modifiers
- `-x, --extension <ext>` : Load a specific extension file (supports shell tab completion).
- `-xargs, --extension-arguments <args>` : Arguments to pass to a command extension.
- `-d, --disown-reading-process` : Detach the reading process from the terminal.
- `-D, --no-disown-reading-process` : Keep the reading process attached to the terminal.
- `--private` : Do not update the recent history list during this session.

---

### Environment Variables

Almost all CLI options can be permanently set in `~/.config/lib-x/config` or overridden using environment variables prefixed with `LIB_X_`.

- `LIB_X_LAUNCHER` (e.g., `fzf` or `rofi`)
- `LIB_X_CALIBRE_LIBRARY_PATH` (e.g., `~/Books`)
- `LIB_X_PREVIEW_ENABLE` (`true` or `false`)
- `LIB_X_PREVIEW_IMAGES_ENABLE` (`true` or `false`)
- `LIB_X_PREVIEW_IMAGES_RENDERER` (`chafa`, `icat`, `imgcat`)
- `LIB_X_FILE_EXPLORER` (`yazi`, `fzf`)
- `LIB_X_COLORS_ENABLE` (`true` or `false`)

---

### Examples & Workflows

**Hello world**
Save your current runtime settings to the config file:
```bash
LIB_X_PREVIEW_IMAGES_RENDERER=icat LIB_X_LAUNCHER=fzf lib-x --preview --preview-images --config-write
```

**Desktop app launcher**
Launch `lib-x` as a graphical application using Rofi:
```bash
lib-x --launcher rofi --preview --disown-reading-process
```

**Quick Search & Read**
Search for chess books, sort by size descending, skip the selection menu, open the book, and exit the CLI:
```bash
lib-x --search "tag:chess" --sort-by "size" --book-skip --read --book-exit
```

**Interactive Custom Reader Configuration**
If you want to use a specific reader depending on the extension:
```bash
export LIB_X_READER="pdf:zathura,epub:foliate,mobi:ebook-viewer"
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
~/.config/lib-x/config
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
| `CONFIG_COLORS_ENABLE`         | `true`              | Enable or disable ANSI true-color formatting in the UI.                |
| `CONFIG_EDITOR`                | `vi` (or `$EDITOR`) | Text editor used for editing configs and files.                        |
| `CONFIG_TERMINAL_EXEC`         | _(auto-detected)_   | The terminal emulator used to spawn interactive shells/apps.           |
| `CONFIG_NOTIFICATION_DURATION` | `3`                 | Duration (in seconds) for desktop/CLI notifications to remain visible. |

#### Media & Covers

| Variable                           | Default | Description                                                                     |
| :--------------------------------- | :------ | :------------------------------------------------------------------------------ |
| `CONFIG_PREVIEW_ENABLE`            | `false` | Enable or disable the preview window (metadata & descriptions).                 |
| `CONFIG_PREVIEW_IMAGES_ENABLE`     | `false` | Whether to render book covers in the preview window.                            |
| `CONFIG_PREVIEW_IMAGES_RENDERER`   | `chafa` | Tool used to render images in the terminal. Options: `chafa`, `icat`, `imgcat`. |
| `CONFIG_PREVIEW_IMAGES_CHAFA_ARGS` | `""`    | Extra arguments for `chafa`.                                                    |
| `CONFIG_PREVIEW_IMAGES_ICAT_ARGS`  | `""`    | Extra arguments for `icat`.                                                     |
| `CONFIG_PREVIEW_IMAGES_IMGCAT_ARGS`| `""`    | Extra arguments for `imgcat`.                                                   |

#### Calibre Handling

| Variable                        | Default             | Description                                                            |
| :------------------------------ | :------------------ | :--------------------------------------------------------------------- |
| `CONFIG_CALIBRE_LIBRARY_PATH`   | `~/Calibre Library` | Absolute path to your active Calibre library folder.                   |
| `CONFIG_FILE_EXPLORER`          | `fzf` (or `yazi`)   | Tool used when selecting "Add Books From Folder".                      |
| `CONFIG_READER`                 | `""`                | Comma-separated list for custom readers (e.g., `pdf:zathura,epub:foliate`). If empty, uses system default. |
| `CONFIG_READING_PROCESS_DISOWN` | `true`              | Run the eBook reader in the background without blocking the UI.        |
| `CONFIG_SORT_BY`                | `""`                | Default sort field (e.g. `size`, `author_sort`). Append `_asc` to reverse. |

#### History & Lists

| Variable                       | Default | Description                                                         |
| :----------------------------- | :------ | :------------------------------------------------------------------ |
| `CONFIG_RECENT_BOOKS_UPDATE`   | `true`  | Save books automatically to the Recent list when you select "Read". |
| `CONFIG_RECENT_BOOKS_LIMIT`    | `30`    | The maximum number of books to retain in your Recent list.          |
| `CONFIG_RANDOM_BOOKS_LIMIT`    | `30`    | Number of books to fetch when generating a Random list.             |
| `CONFIG_SEARCH_HISTORY_ENABLE` | `true`  | Save local search queries to reuse them later.                      |
| `CONFIG_CACHE_RETENTION_DAYS`  | `7`     | Number of days before cleaning up old generated previews/caches.    |

#### Fzf, Gum, and Rofi Configurations

| Variable                    | Description                                                                              |
| :-------------------------- | :--------------------------------------------------------------------------------------- |
| `CONFIG_FZF_OPTS`           | Fine‑tune `fzf` layout, colors, pointers. Defaults to Tokyo Night colors.                |
| `CONFIG_FZF_HEADER`         | The header logo for the `fzf` view.                                                      |
| `CONFIG_GUM_FILTER_OPTS`    | Options passed directly to `gum filter`.                                                 |
| `CONFIG_GUM_INPUT_OPTS`     | Options passed directly to `gum input`.                                                  |
| `CONFIG_GUM_CONFIRM_OPTS`   | Options passed directly to `gum confirm`.                                                |
| `CONFIG_GUM_SPIN_OPTS`      | Options passed directly to `gum spin`.                                                   |
| `CONFIG_ROFI_THEME_MAIN`    | Path to a custom Rofi `.rasi` theme for the main menu.                                   |
| `CONFIG_ROFI_THEME_PREVIEW` | Path to a custom Rofi `.rasi` theme for the preview menu.                                |
| `CONFIG_ROFI_THEME_PROMPT`  | Path to a custom Rofi `.rasi` theme for user text input prompts.                         |
| `CONFIG_ROFI_THEME_CONFIRM` | Path to a custom Rofi `.rasi` theme for confirmation dialogs.                            |
| `CONFIG_ROFI_THEME_PAGER`   | Path to a custom Rofi `.rasi` theme for pager menus (e.g. long text).                    |

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
Add to `~/.config/lib-x/config`:

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
If books aren't showing up, select **Miscellaneous -> Sync Data** in the menu to force a cache refresh.

</details>

<details>
<summary><b>How does lib-x open books? Can I change my reader?</b></summary>
<br>

`lib-x` primarily uses your operating system's native file opener (`open` on macOS, `xdg-open` on Linux, `cmd.exe` on Windows/WSL).
However, you can explicitly map extensions to your preferred readers directly inside the `lib-x` config:
`CONFIG_READER="pdf:zathura,epub:foliate"`

</details>

<details>
<summary><b>Why are my image previews not showing up?</b></summary>
<br>

Image previews require a few components to work together:

1. Ensure you have enabled them in your config: `CONFIG_PREVIEW_ENABLE=true` and `CONFIG_PREVIEW_IMAGES_ENABLE=true`.
2. Ensure you have a supported image renderer installed (e.g., `chafa`, `icat`, or `imgcat`).
3. Set the correct renderer in your config: `CONFIG_PREVIEW_IMAGES_RENDERER="chafa"`.
4. Ensure your terminal emulator actually supports image rendering. If it doesn't, stick with `chafa`, which falls back to excellent ASCII/block character rendering.

</details>

<details>
<summary><b>Previews overlap text or look distorted. How do I fix this?</b></summary>
<br>

If your images are overlapping with UI text, your terminal may not properly support the image clearing sequences used by `chafa`.

1. **Kitty / Ghostty:** Set `CONFIG_PREVIEW_IMAGES_RENDERER="icat"`.
2. **iTerm2 / WezTerm:** Try `CONFIG_PREVIEW_IMAGES_RENDERER="imgcat"`.
3. **Other Terminals:** Stick to `CONFIG_PREVIEW_IMAGES_RENDERER="chafa"`, but ensure your terminal supports Sixel.

</details>

## Contribution

Pull requests are highly welcome :)

### Supporting the Project

If you enjoy using `lib-x` and want to support its ongoing development, **consider leaving a Star on GitHub!**
