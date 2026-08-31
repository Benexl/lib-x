<div align="center">

# 📚 lib-x

**Browse your Calibre Library from your terminal or app launcher.**

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
  - [Scripting & Keybindings](#scripting--keybindings)
  - [Examples & Workflows](#examples--workflows)
- [Configuration](#configuration)
  - [Configuration File Location](#configuration-file-location)
  - [Configuration Variables](#configuration-variables)
- [Full Text Search](#full-text-search)
- [Extensions](#extensions)
- [Frequently Asked Questions (FAQ)](#frequently-asked-questions-faq)
- [Contribution](#contribution)
- [Support](#support)

## Features

- **Multiple Launcher Support**: Browse with `fzf`, `rofi`, or `gum`, all supporting rich previews.
- **Deep Calibre Integration**: Interface securely with your library via `calibredb`. Supports both native and **Flatpak** Calibre installations automatically.
- **Search & Filter**: Search books using Calibre's native syntax, or browse directly by Authors, Series, Tags, Formats, Languages, Ratings, Publishers, and Identifiers.
- **Full Text Search (FTS)**: Search inside the actual content of your books using Calibre's FTS engine. Manage the FTS index (enable, disable, reindex) directly from the Miscellaneous menu.
- **Search History**: Automatically tracks your past search queries for quick recall. Shared across both regular search and FTS search.
- **Personal Reading Lists**: Track your reading journey with built-in user lists (Reading, Paused, Planning, Re-reading, Completed, Dropped, Docs).
- **Extensive Book Actions**: Directly from the terminal:
  - Read your books
  - Edit Metadata (Tags, Authors, Dates, etc.)
  - Convert formats (`ebook-convert`)
  - Polish books (`ebook-polish`)
  - View raw metadata
  - Open in Calibre's GUI Viewer (`ebook-viewer`)
  - Drop into a stateful interactive shell
- **Smart Format Picker**: When a book has multiple formats, choose the right one to read — or set `CONFIG_PREFERRED_BOOK_FMT` / `LIB_X_PREFERRED_BOOK_FMT` to skip the prompt and always read your preferred format directly.
- **Bulk Add Books**: Seamlessly add books from files or folders (integrates with `fzf` or `yazi` as a file chooser).
- **Theming & Styling**: Theming support through `.theme` extensions with Tokyo Night as the default theme.
- **Multi-language Support**: Loadable language files (`.lang`) to localize UI prompts and messages.
- **Cover Art Previews**: High-quality book cover image rendering directly in the terminal using `chafa`, `icat`, or `imgcat`.
- **Custom Readers**: Map specific formats (e.g., EPUB, PDF) to your preferred CLI/GUI reading apps.
- **Scriptable Shortcuts**: Bypass menus and jump straight to specific lists, searches, or actions using direct command-line flags — combinable with `--book-skip`, `--book-exit`, and `--cmd-exit` for fully headless scripting.
- **Direct List Management**: Add/remove books to your reading lists directly from the command line (`--add-to-reading`, `--add-to-completed`, etc.).
- **Dropped Book Filtering**: Automatically hides dropped books from all menus by default (`CONFIG_FILTER_DROPPED`).
- **Stateful Sub-Shell Execution**: Drop into a shell (or run `--shell-exec`) pre-loaded with environment variables of your currently selected book for custom scripting or manual database interactions.
- **Extensible fzf Keybindings**: Ship with built-in binds (`alt-e`, `alt-m`, `alt-r`, `alt-v`) that run book actions straight from the results list, and are fully overridable via `CONFIG_FZF_OPTS`.
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

- `calibre` - Provides `calibredb` for database interactions. Both native and Flatpak installations are supported (Flatpak is auto-detected).
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
- `--search-title <term>` : Search for a book by exact title (literal match, not regex).
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
- `--random` : Browse random books directly.
- `--misc` : Open the miscellaneous menu (Sync, Add books, FTS).

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
- `--shell` : Open an interactive sub-shell pre-loaded with the selected book's state variables.
- `--shell-exec <code>` : Execute a command in a sub-shell pre-loaded with the selected book's state variables (non-interactive, great for scripting & keybindings).

#### Direct List Management (Skip the media action + list menus)

These shortcuts add the selected book directly to a specific list, bypassing the "Manage My Lists" submenu.

- `--add-to-reading` : Add the selected book to your Reading list.
- `--add-to-paused` : Add the selected book to your Paused list.
- `--add-to-planning` : Add the selected book to your Planning list.
- `--add-to-rereading` : Add the selected book to your Re-reading list.
- `--add-to-docs` : Add the selected book to your Docs list.
- `--add-to-completed` : Add the selected book to your Completed list.
- `--add-to-dropped` : Add the selected book to your Dropped list.
- `--remove-from-lists` : Remove the selected book from all your lists.

#### UI & Process Control

- `-l, --launcher <fzf|rofi|gum>` : Override the default menu launcher.
- `--preview` : Enable the preview window (metadata).
- `--no-preview` : Disable the preview window.
- `--preview-images` : Enable the image preview (book covers).
- `--no-preview-images` : Disable the image preview.
- `-d, --disown-reading-process` : Detach the reading process from the terminal (default).
- `-D, --no-disown-reading-process` : Keep the reading process attached to the terminal session.
- `--private` : Do not update the recent history list when opening a book.
- `--manage-my-lists` : Open the list management submenu for the selected book.

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
- `LIB_X_SORT_BY` (e.g., `author`, `size_asc`, `pubdate`)
- `LIB_X_FILTER_DROPPED` (`true` or `false` — hides dropped books from all menus)
- `LIB_X_SEARCH_HISTORY_ENABLE` (`true` or `false`)
- `LIB_X_READER` (e.g., `epub:zathura,pdf:evince`)
- `LIB_X_PREFERRED_BOOK_FMT` (e.g., `epub`, `pdf`)

---

### Scripting & Keybindings

`lib-x` is designed to be composable from the terminal, which makes it a great fit for shell scripts, window-manager keybindings, and extending its own `fzf` interface.

#### Drop into a stateful sub-shell

Selecting **Shell** from the Book Actions menu (or using `--shell`) drops you into a sub-shell pre-loaded with everything about the currently selected book:

```bash
lib-x --shell
```

Inside that shell (and via `--shell-exec`), these variables are exported:

- `STATE_CURRENT_BOOK` - Raw JSON payload (UUIDs, authors, formats, tags)
- `STATE_CURRENT_BOOK_TITLE` - Title of the selected book
- `STATE_CURRENT_CATEGORY` - Current category filter (if any)
- `STATE_CURRENT_BOOKS` - Path to the current book list file
- `STATE_CURRENT` - Current state depth level
- `CALIBRE_DB_JSON_FILE` - Path to the cached database
- `CALIBRE_CATEGORIES_TSV_FILE` - Path to the cached categories file
- `CLI_CURRENT_STATE_DIR` - Path to the current state directory
- `CLI_NAME` - The CLI name (`lib-x`)

You can pipe the book JSON through `jq` to run custom scripts, raw Calibre commands, or manipulate book files without leaving `lib-x`:

```bash
lib-x --shell-exec 'jq -r .title "$STATE_CURRENT_BOOK"'
```

#### Headless chaining for scripts & keybindings

By combining the menu-skip flags with a direct action you can trigger book actions non-interactively — no TUI required:

- `--cmd-exit` (`-ce`) : exit after the shortcut menu command-line options
- `--book-skip` (`-bs`) : skip item selection and auto-pick the first result
- `--book-exit` (`-be`) : exit immediately after the action

For example, to read the first book matching a search without ever seeing a menu:

```bash
lib-x --cmd-exit --book-skip --book-exit --read --search-title "Dune"
```

You can also chain via `--shell-exec` to run arbitrary code for the matched book, or use `--search-title` to target a specific title in one shot.

#### Built-in fzf keybindings

When using the `fzf` launcher, `lib-x` ships sensible keybindings inside its default `CONFIG_FZF_OPTS` so you can act on a book directly from the results list:

| Keybind   | Action              | Command used                                                                      |
| :-------- | :------------------ | :-------------------------------------------------------------------------------- |
| `alt-v`   | Read                | `… --cmd-exit --book-skip --book-exit --read --search-title`                      |
| `alt-e`   | Edit Metadata       | `… --cmd-exit --book-skip --book-exit --edit-metadata --search-title`              |
| `alt-m`   | Manage My Lists     | `… --cmd-exit --book-skip --book-exit --manage-my-lists --search-title`            |
| `alt-r`   | Remove Book         | `… --cmd-exit --book-skip --book-exit --remove-book --search-title`                |
| `ctrl-/`  | Toggle preview      | `toggle-preview`                                                                  |
| `ctrl-space` | Toggle wrap      | `toggle-wrap+toggle-preview-wrap`                                                 |

Each keybind parses the hovered book's title and re-invokes `lib-x` with `LIB_X_SEARCH_HISTORY_ENABLE=false` and the chained flags above, e.g. the read binding expands to:

```bash
LIB_X_SEARCH_HISTORY_ENABLE=false lib-x --cmd-exit --book-skip --book-exit \
  --read --search-title "<hovered book title>"
```

Because `CONFIG_FZF_OPTS` is fully exposed in the generated config file (edit it with `lib-x --edit-config`), you can extend those binds or add your own. Append a `--bind` inside `CONFIG_FZF_OPTS` that calls `$CLI_PATH` the same way — for example, running `--shell-exec` on the hovered book:

```bash
--bind='alt-s:execute(LIB_X_SEARCH_HISTORY_ENABLE=false $CLI_PATH --cmd-exit --book-skip --book-exit --shell-exec "echo read: $STATE_CURRENT_BOOK_TITLE" --search-title "$(printf {} | sed -e "s/^[0-9][0-9]* //g" -e "s/^.*\.env|[0-9][0-9]* //g")")'
```

(Add that line inside the existing `CONFIG_FZF_OPTS="..."` block in your config file, before the closing quote.)

> Tip: any custom bind that should not touch search history can prefix the command with `LIB_X_SEARCH_HISTORY_ENABLE=false`, exactly as the built-ins do.

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
| `CONFIG_FILTER_DROPPED`        | `true`              | Automatically hide books in the "Dropped" list from all menus.         |

#### Previews

| Variable                           | Default | Description                                                                     |
| :--------------------------------- | :------ | :------------------------------------------------------------------------------ |
| `CONFIG_PREVIEW_ENABLE`            | `false` | Enable or disable the preview window (metadata descriptions).                   |
| `CONFIG_PREVIEW_IMAGES_ENABLE`     | `false` | Enable rendering book covers in the preview window.                             |
| `CONFIG_PREVIEW_IMAGES_RENDERER`   | `chafa` | Tool used to render images in the terminal. Options: `chafa`, `icat`, `imgcat`. |
| `CONFIG_PREVIEW_IMAGES_CHAFA_ARGS` | `""`    | Pass custom arguments to `chafa`.                                               |
| `CONFIG_PREVIEW_IMAGES_ICAT_ARGS`  | `""`    | Pass custom arguments to `icat` / `kitty +kitten icat`.                         |
| `CONFIG_PREVIEW_IMAGES_IMGCAT_ARGS`| `""`    | Pass custom arguments to `imgcat`.                                              |

#### Calibre & Book Management

| Variable                      | Default                 | Description                                                                       |
| :---------------------------- | :---------------------- | :-------------------------------------------------------------------------------- |
| `CONFIG_CALIBRE_LIBRARY_PATH` | `~/Calibre Library`     | Absolute path to your Calibre library database directory.                         |
| `CONFIG_FILE_EXPLORER`        | `fzf`                   | File chooser used when adding books to the library. Options: `fzf`, `yazi`.       |
| `CONFIG_READER`               | `""`                    | Mapping of `ext:command` (e.g. `epub:zathura`). Falls back to OS default if empty.|
| `CONFIG_PREFERRED_BOOK_FMT`   | `""`                    | Preferred format (e.g. `epub`, `pdf`) used directly when reading. If unset and the book has multiple formats, a format picker is shown. |
| `CONFIG_READING_PROCESS_DISOWN`| `true`                 | Detach reader process from terminal so `lib-x` can be closed without killing app. |
| `CONFIG_SORT_BY`              | `""`                    | Default sort field (e.g. `author`, `size_asc`, `pubdate`).                        |
| `CONFIG_RANDOM_BOOKS_LIMIT`   | `30`                    | Number of books to return when selecting "Random".                                |

#### History & Caching

| Variable                       | Default | Description                                                                            |
| :----------------------------- | :------ | :------------------------------------------------------------------------------------- |
| `CONFIG_SEARCH_HISTORY_ENABLE` | `true`  | Save local search history to track and quickly recall past queries (shared across search and FTS). |
| `CONFIG_RECENT_BOOKS_UPDATE`   | `true`  | Automatically log opened books to the "Recent" list.                                   |
| `CONFIG_RECENT_BOOKS_LIMIT`    | `30`    | Number of books to keep in the recent history list.                                    |
| `CONFIG_CACHE_RETENTION_DAYS`  | `7`     | Auto-clean stale preview images and shell scripts older than this duration.            |

#### Fzf, Gum, and Rofi

*(Note: Advanced Fzf and Gum styling parameters are also exposed in the config file. See the generated config file for full default strings).*

| Variable                    | Default        | Description                                                                 |
| :-------------------------- | :------------- | :-------------------------------------------------------------------------- |
| `CONFIG_FZF_HEADER`         | _(logo)_       | Custom ASCII logo displayed at the top of the `fzf` menu.                   |
| `CONFIG_FZF_OPTS`           | _(see config)_ | Fine‑tune `fzf` layout, colors, and bindings. Defaults to "Tokyo Night".    |
| `CONFIG_GUM_CONFIRM_OPTS`   | _(see config)_ | Custom `gum confirm` styling options (foregrounds, colors).                 |
| `CONFIG_GUM_FILTER_OPTS`    | _(see config)_ | Custom `gum filter` styling options (prompt, indicator, match highlighting).|
| `CONFIG_GUM_INPUT_OPTS`     | _(see config)_ | Custom `gum input` styling options (prompt, cursor, placeholder).           |
| `CONFIG_GUM_PAGER_OPTS`     | _(see config)_ | Custom `gum pager` styling options (line numbers, match highlighting).      |
| `CONFIG_GUM_SPIN_OPTS`      | _(see config)_ | Custom `gum spin` styling options (spinner type, title).                    |
| `CONFIG_ROFI_THEME_MAIN`    | `""`           | Path to a custom Rofi `.rasi` theme for the main menu.                      |
| `CONFIG_ROFI_THEME_PREVIEW` | `""`           | Path to a custom Rofi `.rasi` theme for the preview menu.                   |
| `CONFIG_ROFI_THEME_PROMPT`  | `""`           | Path to a custom Rofi `.rasi` theme for prompt dialogs.                     |
| `CONFIG_ROFI_THEME_CONFIRM` | `""`           | Path to a custom Rofi `.rasi` theme for confirmation dialogs.               |
| `CONFIG_ROFI_THEME_PAGER`   | `""`           | Path to a custom Rofi `.rasi` theme for the pager.                          |

## Full Text Search

`lib-x` integrates with Calibre's Full Text Search (FTS) engine, allowing you to search inside the actual content of your books — not just titles, authors, or tags.

### Accessing FTS

Navigate to **Miscellaneous > Full Text Search** from the main menu, or use the **Miscellaneous > Manage FTS Index** submenu to control the index.

### FTS Index Management

Before using FTS, you need to enable and build the index. From the **Manage FTS Index** submenu, you can:

| Action                          | Description                                                        |
| :------------------------------ | :----------------------------------------------------------------- |
| **Show Indexing Status**        | View the current state of the FTS index.                           |
| **Enable FTS Indexing**         | Enable the FTS index for your library.                             |
| **Disable FTS Indexing**        | Disable the FTS index.                                             |
| **Re-index Library**            | Start re-indexing the library in the background.                   |
| **Re-index Library (wait)**     | Re-index and block until the process completes.                    |

### Searching

Once the index is enabled, select **Full Text Search** from the Miscellaneous menu. You will be prompted to enter a search query. Results are presented in the same book explorer UI as all other searches.

FTS queries support Calibre's full text search syntax. See the [Calibre manual](https://manual.calibre-ebook.com/gui.html#full-text-search) for details on query syntax.

> **Note:** FTS indexing is resource-intensive for large libraries. It is recommended to index in the background and only re-index after adding or modifying a significant number of books.

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
- `STATE_CURRENT_BOOK_TITLE` - Title of the selected book
- `STATE_CURRENT_BOOK` - Raw JSON payload containing UUIDs, authors, formats, tags
- `STATE_CURRENT_BOOKS` - Path to the current book list file
- `STATE_CURRENT_CATEGORY` - Current category filter (if any)
- `STATE_CURRENT` - Current state depth level
- `CALIBRE_DB_JSON_FILE` - Path to the cached database
- `CALIBRE_CATEGORIES_TSV_FILE` - Path to the cached categories file
- `CLI_CURRENT_STATE_DIR` - Path to the current state directory
- `CLI_NAME` - The CLI name (`lib-x`)

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

<details>
<summary><b>Does lib-x work with Flatpak Calibre?</b></summary>
<br>

Yes. `lib-x` automatically detects Flatpak Calibre installations (the `com.calibre_ebook.calibre` Flatpak package). When detected, all Calibre commands (`calibredb`, `ebook-viewer`, `ebook-convert`, etc.) are executed through `flatpak run` transparently. No manual configuration is required.

</details>

<details>
<summary><b>How does Full Text Search (FTS) work?</b></summary>
<br>

FTS uses Calibre's built-in full text search engine to index the content of your books. You must first enable and build the index from **Miscellaneous > Manage FTS Index**. Once indexed, you can search inside book contents from **Miscellaneous > Full Text Search**. The index is stored by Calibre alongside your library database. Note that indexing can be resource-intensive for large libraries.

</details>

<details>
<summary><b>How do I prevent dropped books from showing in menus?</b></summary>
<br>

By default, `lib-x` automatically hides books in your "Dropped" list from all menus. This is controlled by the `CONFIG_FILTER_DROPPED` variable (default: `true`). To show dropped books in all menus, set `CONFIG_FILTER_DROPPED=false` in your config file.

</details>

## Contribution

Pull requests are highly welcome! :)

### Supporting the Project

If you enjoy using `lib-x` and want to support its ongoing development, **consider leaving a Star on GitHub!**
