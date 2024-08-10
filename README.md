# bfp - batch file processor

## Description

This bash script performs various operations on files in the current directory, including unzipping, removing duplicates, renaming, stripping metadata, converting image formats, and cleaning up small files.

## Features

- Unzips all ZIP files in the current directory
- Removes duplicate files using `rmlint`
- Renames files (requires `bfr` tool)
- Strips metadata from files using `exiftool`
- Removes files smaller than 100KB
- Converts WEBP files to PNG or GIF based on their content
- Converts small JPEG files (< 1MB) to PNG
- Removes EXIF data from newly converted files
- Performs a final cleanup of files smaller than 1MB

## Prerequisites

Ensure you have the following tools installed on your Arch Linux system:

- `unzip`
- `rmlint`
- `bfr` (batch file renamer)
- `exiftool`
- `imagemagick`

You can install most of these using pacman:

```bash
sudo pacman -S unzip rmlint perl-image-exiftool imagemagick
```

Note: You may install `bfr` via [https://github.com/za08/bfr]

## Usage

1. Place the script in the directory containing the files you want to process.
2. Make the script executable:
   ```bash
   chmod +x file_processor.sh
   ```
3. Run the script:
   ```bash
   ./file_processor.sh
   ```

## Warning

This script performs destructive operations on files in the current directory. It will:
- Delete original ZIP files after extraction
- Remove duplicate files
- Delete small files
- Convert image formats
- Strip metadata and EXIF data

Always run this script on a copy of your data, not the original files.

## Contributing

Feel free to fork this repository and submit pull requests with improvements or bug fixes.

## License

[MIT License](https://opensource.org/licenses/MIT)

## Disclaimer

Use this script at your own risk. The author is not responsible for any data loss or damage caused by the use of this script.
