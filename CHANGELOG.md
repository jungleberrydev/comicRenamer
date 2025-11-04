# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Initial project setup with git repository
- Comprehensive README documentation
- `.env.example` template file for configuration

### Changed

- Switched from hardcoded external directory path to environment variable configuration
- Added `.env` file support with fallback to environment variables

## [1.0.0] - Initial Release

### Added

- Comic renaming script (`rename_comics.py`)
  - Smart filename parsing for multiple formats:
    - Issues: `Title #001 (2025)`, `Title 001 (2019)`, etc.
    - Volumes: `Title v02 (2012)`, `Title Vol. 2 (2012)`, etc.
    - Standalone comics: `Title (2025)`, `Title - Subtitle (2024)`, etc.
  - Automatic organization into folders by title
  - Duplicate detection against external comics directory
  - Case-insensitive filename matching
  - Extension-agnostic duplicate checking (`.cbz` vs `.cbr`)
  - Dry-run mode for previewing changes
  - Verbose output option
  - Error handling with unparseable files moved to `error/` directory
  - Summary reports with statistics and error/duplicate lists
  - Support for `.cbz` and `.cbr` file formats

### Configuration

- Environment variable support: `COMIC_SORTER_EXTERNAL_DIR`
- `.env` file support (checked first, then falls back to environment variable)
- Configuration is optional - script works without duplicate detection

### Documentation

- Comprehensive README with usage examples
- Installation instructions
- Configuration guide
- Examples of supported filename formats

### Files

- `rename_comics.py` - Main script
- `.gitignore` - Ignores Python cache, working directories, personal files, and `.env` files
- `.env.example` - Configuration template

[Unreleased]: https://github.com/jungleberrydev/comicRenamer/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/jungleberrydev/comicRenamer/releases/tag/v1.0.0
