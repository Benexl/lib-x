<div align="center">

# 📚 lib-x

**Manage and read your calibre books from the terminal or app launcher.**

[![GitHub Issues or Pull Requests](https://img.shields.io/github/issues/Benexl/lib-x?style=flat-square)](https://github.com/Benexl/lib-x/issues)
[![GitHub License](https://img.shields.io/github/license/Benexl/lib-x?style=flat-square)](https://github.com/Benexl/lib-x/blob/master/LICENSE)
[![GitHub file size in bytes](https://img.shields.io/github/size/Benexl/lib-x/lib-x?style=flat-square)]()
![GitHub Downloads (specific asset, all releases)](https://img.shields.io/github/downloads/Benexl/lib-x/lib-x?displayAssetName=false&style=flat-square&color=%2397ca00)
[![GitHub Release](https://img.shields.io/github/v/release/Benexl/lib-x?style=flat-square)](https://github.com/Benexl/lib-x/releases)
[![GitHub commit activity](https://img.shields.io/github/commit-activity/m/Benexl/lib-x?style=flat-square)]()

</div>

[lib-x demo](https://github.com/user-attachments/assets/placeholder-for-your-demo-video.webm)

<details>
<summary><b>View Demos & Previews</b></summary>

**Full Demo:**

[lib-x-full-github-demo.webm](https://github.com/user-attachments/assets/placeholder-for-your-demo-video.webm)

**Previews:**

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/placeholder-image-1" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/placeholder-image-2" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/placeholder-image-3" />

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
- [Frequently Asked Questions (FAQ)](#frequently-asked-questions-faq)
- [Contribution](#contribution)
- [Support](#support)

## Features

- **Multiple Launcher Support**: Browse with `fzf`, `rofi`, or `gum`, all supporting rich previews.
- **Deep Calibre Integration**: Interface securely with your library via `calibredb`.
- **Search & Filter**: Search books using Calibre's native syntax, or browse directly by Authors, Series, Tags, Formats, Languages, Ratings, Publishers, and Identifiers.
- **Personal Reading Lists**: Track your reading journey with built-in user lists (Reading, Paused, Planning, Re-reading, Completed, Dropped, Docs).
- **Extensive Book Actions**: Directly from the terminal:
  - Read your books
  - Edit Metadata (Tags, Authors, Dates, etc.)
  - Convert formats (`ebook-convert`)
  - Polish books (`ebook-polish`)
  - View raw metadata
  - Open in Calibre's GUI Viewer (`ebook-viewer`)
- **Bulk Add Books**: Seamlessly add books from files or folders (integrates with `fzf` or `yazi` as a file chooser).
- **Theming & Styling**: Theming support through `.theme` extensions with Tokyo Night as the default theme.
- **Multi-language Support**: Loadable language files (`.lang`) to localize UI prompts and messages.
- **Cover Art Previews**: High-quality book cover image rendering directly in the terminal using `chafa`, `icat`, or `imgcat`.
- **Custom Readers**: Map specific formats (e.g., EPUB, PDF) to your preferred CLI/GUI reading apps.
- **Scriptable Shortcuts**: Bypass menus and jump straight to specific lists, searches, or actions using direct command-line flags.
- **Stateful Sub-Shell Execution**: Drop into a shell pre-loaded with environment variables of your currently selected book for custom scripting or manual database interactions.
- **Desktop Integration**: Generate a `.desktop` file to launch natively from application menus (Linux).
- **Cache Management**: Automatically caches your Calibre database as JSON for lightning-fast speeds, cleaning up stale previews and data automatically (Default: 7 days).
- **OS Support**: Works across Linux, macOS, Windows (via WSL/MSYS/Cygwin), and Android (Termux).
- **Auto-Updater**: Secure update checker that pulls the latest version from GitHub and shows you the diff before applying.
- **Shell Completions**: Includes tab completions for `fish`, `bash`, and `zsh` covering flags, custom categories, and book sorting options.

## Installation

![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![macOS](https://img.shields.io/badge/macOS-000000?style=flat-square&logo=apple&logoColor=white)
![Windows](https://img.shields.io/badge/Windows-0078D6?style=flat-square&logo=windows&logoColor=white)
![Android](https://img.shields.io/badge/Android-3DDC84?style=flat-square&logo=android&logoColor=white)
![Arch Linux](https://img.shields.io/badge/Arch_Linux-1793D1?style=flat-square&logo=arch-linux&logoColor=white)
![NixOS](https://img.shields.io/badge/NixOS-5277C3?style=flat-square&logo=nixos&logoColor=white)

### Prerequisites

**Required:**

- `calibre` - Provides `calibredb` for database interactions.
- `fzf` - Main terminal launcher.
- `jq` - For rapid JSON database parsing.
- `sh` - Any POSIX-compliant shell (Bash, Zsh, Dash, etc.).
- **Nerd Font** - For the icons (Recommended: JetBrains Mono Nerd Font).

**Optional (Highly Recommended for Full Functionality):**

- **Terminal File Explorers (For adding books):** `yazi` or `fzf`
- **Calibre CLI Tools:** `ebook-convert`, `ebook-polish`, `ebook-viewer`, `ebook-meta`, `ebook-edit` (Usually bundled with Calibre).
- **Alternate Launchers:** `rofi` (for a desktop app experience) or `gum` (for styled TUI flows).
- **Modern Terminal That Supports True Color:** `kitty`, `ghostty`, `wezterm`, etc.
- **Terminal Image Viewers (For Cover Art):**
  - `chafa` _(Cross-terminal)_
  - `icat` _(Recommended for Kitty and Ghostty)_
  - `imgcat` _(For iTerm2/WezTerm)_
- **Terminal QoL:**
  - `bat` _(Better paging and diff viewing)_

---

### Universal Installation

Ensure `~/.local/bin` exists and is added to your system's `$PATH`.

```bash
curl -sL "https://github.com/Benexl/lib-x/releases/download/v0.5.0/lib-x" -o ~/.local/bin/lib-x
chmod +x ~/.local/bin/lib-x
```

_To uninstall, just run: `rm ~/.local/bin/lib-x`_, then to remove its related data folders `rm -r ~/.config/lib-x` and `rm -r ~/.cache/lib-x`.

---

### Platform-Specific Instructions

Note: I am not the one who maintains any of these packages and you should probably turn off auto updates in `lib-x` if using them.

<details>
<summary><b>Arch Linux (AUR)</b></summary>

```bash
yay -S lib-x-git

# or if you prefer paru

paru -S lib-x-git
```

</details>

<details>
<summary><b>Nix / NixOS</b></summary>

**1. Imperative:**

```bash
nix profile install github:Benexl/lib-x
```

**2. Declarative:**
First, add the repository to your `flake.nix` inputs:

```nix
inputs = {
  nixpkgs.url = "github:nixos/nixpkgs/nixos-unstable";
  lib-x = {
    url = "github:Benexl/lib-x";
    inputs.nixpkgs.follows = "nixpkgs";
  };
}
```

- **For system-wide installation** (in `configuration.nix`):

  ```nix
  environment.systemPackages = [ inputs.lib-x.packages."${system}".default ];
  ```

- **For user-level installation** (via Home Manager in `home.nix`):
  ```nix
  home.packages = [ inputs.lib-x.packages."${system}".default ];
  ```

</details>

## Usage

You can opt to either use it via interactive menus or command-line shortcuts for scripting and keybinding.

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

- `-s, --search <term>` : Prompt for (or immediately execute) a book search.
- `-S, --sort-by <field>` : Sort the books by a specific field (e.g., `author`, `size`, `timestamp`). Append `_asc` for ascending order (default is descending).
- `-r, --no-of-random-books <num>` : Display a specific number of random books from your library.

#### Direct Shortcuts (Skip main menus)

All these options can be paired with `--cmd-exit` (`-ce`) so that backing out of the menu exits the CLI entirely.

- `--reading-list` : Open your actively reading list.
- `--recent` : Show recently opened books.
- `--paused` : Open paused books.
- `--rereading` : Open books marked for re-reading.
- `--planning` : Open planned/to-read books.
- `--completed` : Open completed books.
- `--docs` : Open your documents list.
- `--dropped` : Open dropped/abandoned books.
- `--all` : Browse your entire Calibre library directly.
- `--misc` : Open the miscellaneous menu (Sync, Add books).

#### Book Action Shortcuts (Skip the media action menu)

Can be paired with `--book-skip` (`-bs`) to auto-select the first result, and `--book-exit` (`-be`) to exit immediately after the action.

- `--read` : Open the selected book in your preferred reader.
- `--edit-metadata` : Start editing the metadata for a book.
- `--remove-book` : Delete a book from the library.
- `--viewer` : Open in the Calibre GUI ebook-viewer.
- `--convert` : Convert the book to another format.
- `--edit-book` : Open in the Calibre eBook Editor.
- `--polish` : Run `ebook-polish` on the selected book.
- `--show-metadata` : View the raw metadata (using `ebook-meta`).

#### UI & Process Control

- `-l, --launcher <fzf|rofi|gum>` : Override the default menu launcher.
- `--preview` : Enable the preview window (metadata).
- `--no-preview` : Disable the preview window.
- `--preview-images` : Enable the image preview (book covers).
- `--no-preview-images` : Disable the image preview.
- `-d, --disown-reading-process` : Detach the reading process from the terminal (default).
- `-D, --no-disown-reading-process` : Keep the reading process attached to the terminal session.
- `--private` : Do not update the recent history list when opening a book.

#### Rofi specific

Note: You can find preconfigured rofi themes in the GitHub repo to elevate the desktop app experience!

- `--rofi-theme-main <path>`
- `--rofi-theme-preview <path>`
- `--rofi-theme-prompt <path>`
- `--rofi-theme-confirm <path>`
- `--rofi-theme-pager <path>`

#### Others

- `-x, --extension <ext>` : Load a specific extension file.
- `-xargs, --extension-arguments <args>` : Pass arguments to a loaded extension.
- `-e, --edit-config` : Open the `lib-x` configuration file in your `$EDITOR`.
- `-U, --update` : Check for and apply the latest script update from GitHub.
- `-E, --generate-desktop-entry` : Print a `.desktop` application entry to `stdout`.
- `-v, --version` : Print version information and exit.
- `-h, --help` : Show the help message and exit.
- `--config-write` : Write the current runtime config to the config file.

---

### Environment Variables

Almost all CLI options can be permanently set in `~/.config/lib-x/config` or overridden using environment variables.

- `LIB_X_LAUNCHER` (e.g., `fzf`, `rofi`, `gum`)
- `LIB_X_CALIBRE_LIBRARY_PATH` (e.g., `$HOME/Documents/Calibre Library`)
- `LIB_X_PREVIEW_ENABLE` (`true` or `false`)
- `LIB_X_PREVIEW_IMAGES_ENABLE` (`true` or `false`)
- `LIB_X_PREVIEW_IMAGES_RENDERER` (`chafa`, `icat`, `imgcat`)
- `LIB_X_FILE_EXPLORER` (`fzf`, `yazi`)

---

### Examples & Workflows

**Hello world (Save config)**

```bash
# always put --config-write at the end to save the runtime config
LIB_X_PREVIEW_IMAGES_RENDERER=icat lib-x --preview --preview-images --config-write
```

**Desktop App Launcher**

Launch `lib-x` as a graphical application using Rofi (great with keybindings!).

```bash
lib-x --launcher rofi --preview --preview-images --disown-reading-process
```

**Custom Book Reader Mapping**

You want EPUBs to open in `zathura` and PDFs to open in `evince`. Set this in your config or env:

```bash
LIB_X_READER="epub:zathura,pdf:evince" lib-x --read
```

**Jump straight to your current reads**

```bash
lib-x --reading-list --cmd-exit
```

**Find a specific author and exit menu on back**

```bash
lib-x -s "Isaac Asimov" --cmd-exit
```

**Create a desktop entry**

```bash
lib-x -E > ~/.local/share/applications/lib-x.desktop
```

**Shell completions (Fish)**

```bash
lib-x completions --fish > ~/.config/fish/completions/lib-x.fish
```

## Configuration

By default, the main configuration file is located at:

```bash
~/.config/lib-x/config
```

_(Note: It respects the `$XDG_CONFIG_HOME` environment variable if set)._

You can open it directly using the CLI:

```bash
lib-x --edit-config
```

---

### Configuration Variables

#### Display & Interface

| Variable                       | Default             | Description                                                            |
| :----------------------------- | :------------------ | :--------------------------------------------------------------------- |
| `CONFIG_LAUNCHER`              | `fzf`               | The menu launcher tool to use. Options: `fzf`, `rofi`, `gum`.          |
| `CONFIG_COLORS_ENABLE`         | `true`              | Enable or disable ANSI true-color (24-bit) formatting in the UI.       |
| `CONFIG_EDITOR`                | `vi` (or `$EDITOR`) | Text editor used for editing config files, histories, and metadata.    |
| `CONFIG_NOTIFICATION_DURATION` | `3`                 | Duration (in seconds) for desktop/CLI notifications to remain visible. |
| `CONFIG_TERMINAL_EXEC`         | _auto-detected_     | The terminal emulator used to launch external interactive shell tools. |

#### Previews

| Variable                           | Default | Description                                                                     |
| :--------------------------------- | :------ | :------------------------------------------------------------------------------ |
| `CONFIG_PREVIEW_ENABLE`            | `false` | Enable or disable the preview window (metadata descriptions).                   |
| `CONFIG_PREVIEW_IMAGES_ENABLE`     | `false` | Enable rendering book covers in the preview window.                             |
| `CONFIG_PREVIEW_IMAGES_RENDERER`   | `chafa` | Tool used to render images in the terminal. Options: `chafa`, `icat`, `imgcat`. |
| `CONFIG_PREVIEW_IMAGES_CHAFA_ARGS` | `""`    | Pass custom arguments to `chafa`.                                               |
| `CONFIG_PREVIEW_IMAGES_ICAT_ARGS`  | `""`    | Pass custom arguments to `icat` / `kitty +kitten icat`.                         |

#### Calibre & Book Management

| Variable                      | Default                 | Description                                                                       |
| :---------------------------- | :---------------------- | :-------------------------------------------------------------------------------- |
| `CONFIG_CALIBRE_LIBRARY_PATH` | `~/Calibre Library`     | Absolute path to your Calibre library database directory.                         |
| `CONFIG_FILE_EXPLORER`        | `fzf`                   | File chooser used when adding books to the library. Options: `fzf`, `yazi`.       |
| `CONFIG_READER`               | `""`                    | Mapping of `ext:command` (e.g. `epub:zathura`). Falls back to OS default if empty.|
| `CONFIG_READING_PROCESS_DISOWN`| `true`                 | Detach reader process from terminal so `lib-x` can be closed without killing app. |
| `CONFIG_SORT_BY`              | `""`                    | Default sort field (e.g. `author`, `size_asc`, `pubdate`).                        |
| `CONFIG_RANDOM_BOOKS_LIMIT`   | `30`                    | Number of books to return when selecting "Random".                                |

#### History & Caching

| Variable                       | Default | Description                                                                            |
| :----------------------------- | :------ | :------------------------------------------------------------------------------------- |
| `CONFIG_SEARCH_HISTORY_ENABLE` | `true`  | Save local search history to track and quickly recall past queries.                    |
| `CONFIG_RECENT_BOOKS_UPDATE`   | `true`  | Automatically log opened books to the "Recent" list.                                   |
| `CONFIG_RECENT_BOOKS_LIMIT`    | `30`    | Number of books to keep in the recent history list.                                    |
| `CONFIG_CACHE_RETENTION_DAYS`  | `7`     | Auto-clean stale preview images and shell scripts older than this duration.            |

#### Fzf, Gum, and Rofi

*(Note: Advanced Fzf and Gum styling parameters are also exposed in the config file. See the generated config file for full default strings).*

| Variable                    | Default        | Description                                                                 |
| :-------------------------- | :------------- | :-------------------------------------------------------------------------- |
| `CONFIG_FZF_HEADER`         | _(logo)_       | Custom ASCII logo displayed at the top of the `fzf` menu.                   |
| `CONFIG_FZF_OPTS`           | _(see config)_ | Fine‑tune `fzf` layout, colors, and bindings. Defaults to "Tokyo Night".    |
| `CONFIG_ROFI_THEME_MAIN`    | `""`           | Path to a custom Rofi `.rasi` theme for the main menu.                      |
| `CONFIG_ROFI_THEME_PREVIEW` | `""`           | Path to a custom Rofi `.rasi` theme for the preview menu.                   |
| `CONFIG_ROFI_THEME_PROMPT`  | `""`           | Path to a custom Rofi `.rasi` theme for prompt dialogs.                     |
| `CONFIG_ROFI_THEME_CONFIRM` | `""`           | Path to a custom Rofi `.rasi` theme for confirmation dialogs.               |
| `CONFIG_ROFI_THEME_PAGER`   | `""`           | Path to a custom Rofi `.rasi` theme for the pager.                          |

## Extensions

`lib-x` supports **extensions** to add languages, themes, or override functionality.
Extensions are standard shell scripts loaded from `~/.config/lib-x/extensions/`.

- **Languages:** Add localizations by editing `langs/default.lang` (e.g., swap out `TXT_MENU_MAIN_SEARCH="Search"` to your native language).
- **Themes:** Tweak terminal colors by editing `themes/default.theme` (defines `$THEME_HEADER_COLOR`, `$THEME_FZF_ICON_COLOR_PRIMARY`, etc.).
- **Autoloading:** Add any custom `.sh` script names to `CONFIG_AUTOLOADED_EXTENSIONS="custom.sh"` to have them sourced at runtime.

## Frequently Asked Questions (FAQ)

<details>
<summary><b>Reporting Bugs</b></summary>
<br>

`lib-x` is a wrapper around the powerful `calibredb` command-line utility. 
Before opening an issue, check if the underlying issue is Calibre related:
- **Database syncing / Book adding fails:** Ensure `calibredb` works directly from your terminal. 
- **Metadata parsing or navigation logic fails:** This is handled by `lib-x`. Please open an issue!

</details>

<details>
<summary><b>Where is my Calibre Database located?</b></summary>
<br>

By default, `lib-x` looks in `~/Calibre Library`. If your library is elsewhere, change the `CONFIG_CALIBRE_LIBRARY_PATH` variable in your config file (via `lib-x -e`).
The script specifically looks for the `metadata.db` file in this directory to track modifications.

</details>

<details>
<summary><b>How do I read EPUBs or PDFs in specific apps?</b></summary>
<br>

By default, `lib-x` uses your OS's default file opener (`xdg-open`, `open`, etc.). 
If you want to enforce specific readers, use the `CONFIG_READER` variable formatted as `extension:command,extension2:command2`.

Example: `CONFIG_READER="epub:zathura,pdf:evince,mobi:foliate"`

</details>

<details>
<summary><b>Why are my book covers (image previews) not showing up?</b></summary>
<br>

Image previews require a few components to work together:

1. Ensure you have enabled them in your config: `CONFIG_PREVIEW_ENABLE=true` and `CONFIG_PREVIEW_IMAGES_ENABLE=true`.
2. Ensure you have a supported image renderer installed (e.g., `chafa`, `icat`, or `imgcat`).
3. Set the correct renderer in your config: `CONFIG_PREVIEW_IMAGES_RENDERER="chafa"`.
4. Ensure your terminal emulator actually supports image rendering. If it doesn't, `chafa` is highly recommended as it falls back to excellent ASCII/block character rendering.

</details>

<details>
<summary><b>What is the `--shell` action in the Book Actions menu?</b></summary>
<br>

Selecting `Shell` from a book's action menu drops you into a subshell pre-loaded with all the data about that book. 

Variables exported include:
- `STATE_CURRENT_BOOK_TITLE`
- `STATE_CURRENT_BOOK` (Raw JSON payload containing UUIDs, authors, formats, tags)
- `CALIBRE_DB_JSON_FILE` (Path to the cached database)

This is incredibly powerful if you want to run custom scripts, write raw Calibre commands, or manipulate the book file manually without leaving `lib-x`. Use `jq` to parse the `$STATE_CURRENT_BOOK` payload.

</details>

<details>
<summary><b>How does "Add Books from Folder" work with Yazi?</b></summary>
<br>

If you have `yazi` installed and set `CONFIG_FILE_EXPLORER="yazi"`, selecting "Add Books From Folder" (in the Miscellaneous menu) will launch `yazi`. 
Navigate to the directory you want to import, press `ENTER`, and `lib-x` will automatically pass that directory to `calibredb add` along with any custom options you specify in the subsequent prompt.

</details>

<details>
<summary><b>How do I customize the Nerd Font icons?</b></summary>
<br>

All icons are defined in the language variables (`TXT_ICON_MENU_MAIN_SEARCH`, `TXT_ICON_MENU_BOOK_ACTIONS_READ`, etc.). 
If you don't like them or your terminal doesn't support Nerd Fonts, create a custom `.lang` extension in `~/.config/lib-x/extensions/langs/` and override these variables with empty strings or standard ASCII characters. Load it via `CONFIG_AUTOLOADED_EXTENSIONS`.

</details>

## Contribution

Pull requests are highly welcome! :)

### Supporting the Project

If you enjoy using `lib-x` and want to support its ongoing development, **consider leaving a Star on GitHub!**
