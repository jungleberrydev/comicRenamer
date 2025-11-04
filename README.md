# Comic Renamer

A Python script to automatically rename and organize comic book files (`.cbz` and `.cbr`) into a consistent, normalized format. The script intelligently parses various filename formats and organizes comics into folders by title, with built-in duplicate detection against an external comics directory.

## Features

- **Smart filename parsing** - Handles multiple filename formats:

  - Issues: `Title #001 (2025)`, `Title 001 (2019)`, `Title #1 (2019)`, etc.
  - Volumes: `Title v02 (2012)`, `Title Vol. 2 (2012)`, etc.
  - Standalone comics: `Title (2025)`, `Title - Subtitle (2024)`, etc.
  - Files without years or issue numbers

- **Automatic organization** - Groups comics into folders by title

- **Duplicate detection** - Checks against an external comics directory (ignores file extensions)

- **Case-insensitive matching** - Works regardless of filename capitalization

- **Dry-run mode** - Preview changes before applying them

- **Error handling** - Moves unparseable files to an `error/` directory

- **Summary reports** - Shows detailed statistics and lists of errors/duplicates

## Requirements

- Python 3.6 or higher
- No external dependencies (uses only standard library)

## Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/jungleberrydev/comicRenamer.git
   cd comicRenamer
   ```

2. (Optional) Set up the external comics directory for duplicate detection:

   ```bash
   export COMIC_SORTER_EXTERNAL_DIR="/path/to/your/external/comics"
   ```

   To make this permanent, add it to your shell profile (e.g., `~/.zshrc` or `~/.bashrc`):

   ```bash
   echo 'export COMIC_SORTER_EXTERNAL_DIR="/path/to/your/external/comics"' >> ~/.zshrc
   ```

## Usage

### Basic Usage

```bash
python3 rename_comics.py [directory]
```

If no directory is specified, it defaults to the current working directory.

### Options

- `--dry-run` - Preview changes without modifying files
- `--verbose` or `-v` - Show detailed output for each file processed

### Examples

```bash
# Process current directory
python3 rename_comics.py

# Process a specific directory
python3 rename_comics.py /path/to/comics

# Preview changes first (recommended)
python3 rename_comics.py --dry-run

# Verbose output
python3 rename_comics.py --verbose
```

## Filename Format Support

The script recognizes and normalizes various filename patterns:

### Issues

- `Batman #001 (2025).cbz` → `Batman/Batman #001 (2025).cbz`
- `Batman 001 (2019).cbr` → `Batman/Batman #001 (2019).cbr`
- `Spider-Man #1 (2020).cbz` → `Spider-Man/Spider-Man #001 (2020).cbz`
- `Title 02 (of 04) (2025).cbz` → `Title/Title #002 (2025).cbz`

### Volumes

- `Watchmen v02 (2012).cbr` → `Watchmen/Watchmen Vol. 2 (2012).cbr`
- `Saga Vol. 1 (2012).cbz` → `Saga/Saga Vol. 1 (2012).cbz`

### Standalone

- `Batman Annual (2025).cbz` → `Batman Annual/Batman Annual (2025).cbz`
- `Special Edition (2024).cbr` → `Special Edition/Special Edition (2024).cbr`

## Output Organization

The script organizes files as follows:

```
directory/
├── Title Name/
│   ├── Title Name #001 (2025).cbz
│   ├── Title Name #002 (2025).cbz
│   └── Title Name Vol. 1 (2020).cbz
├── error/
│   └── (unparseable files)
└── possibleDuplicates/
    └── (folders containing duplicates)
```

## Duplicate Detection

The script checks for duplicates by:

1. Comparing filenames (without extensions) against the external comics directory
2. Matching by title folder and issue number
3. Case-insensitive comparison
4. Moving entire title folders to `possibleDuplicates/` if any duplicates are found

**Note:** Duplicate detection is optional. If the `COMIC_SORTER_EXTERNAL_DIR` environment variable is not set, the script will automatically skip duplicate checking and work normally.

## Configuration

### Environment Variable (Optional)

Duplicate detection is **completely optional**. If you don't want to check for duplicates, you can simply leave the `COMIC_SORTER_EXTERNAL_DIR` environment variable unset. The script will work normally and skip duplicate checking.

If you want to enable duplicate detection, set `COMIC_SORTER_EXTERNAL_DIR` to point to your main comics collection directory:

```bash
export COMIC_SORTER_EXTERNAL_DIR="/Volumes/External Drive/Comics"
```

This directory is used for duplicate detection. The script will check if files with the same title and issue number already exist there (ignoring file extensions like `.cbz` vs `.cbr`). If the environment variable is not set or the directory doesn't exist, duplicate checking is automatically skipped.

## Output

The script provides a summary at the end:

```
Renamed: 45  Skipped: 12  Moved to error: 3  Possible duplicates: 8

================================================================================

🔄 POSSIBLE DUPLICATES:
--------------------------------------------------------------------------------
  1. Batman #001 (2025).cbz → Batman #001 (2025).cbz
  2. Spider-Man #005 (2024).cbr → Spider-Man #005 (2024).cbr
  ...

  Total: 8 file(s)

📋 ERRORS (Unparseable files):
--------------------------------------------------------------------------------
  1. corrupted_file.cbz
  2. weird_format.txt
  ...

  Total: 3 file(s)
================================================================================
```

## File Extensions

Supported formats:

- `.cbz` (Comic Book ZIP)
- `.cbr` (Comic Book RAR)

## Tips

1. **Always use `--dry-run` first** to preview changes before processing
2. **Use `--verbose`** to see detailed information about each file
3. **Back up your files** before running the script (especially on large collections)
4. **Set the external directory** environment variable for duplicate detection

## License

This project is open source and available for use.

## Contributing

Contributions are welcome! Feel free to open issues or submit pull requests.
