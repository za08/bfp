# CFP: Comprehensive File Processor

## Overview

This Bash script automates various file processing tasks, including unzipping files, removing duplicates, renaming files, stripping metadata, converting image formats, and deleting small files. It's designed to process a directory of files, performing multiple operations to organize and optimize the content.

## Requirements

- Bash shell
- `unzip` command
- `rmlint` tool
- `ren` command (for file renaming)
- `exiftool` command
- `ImageMagick` suite (`identify` and `magick` commands)

Ensure all these tools are installed and accessible in your system's PATH before running the script.

## Functionality

The script performs the following operations in sequence:

1. **Unzip Files**: Extracts all ZIP files in the current directory and removes the original ZIP files.

2. **Remove Duplicates (First Pass)**: Uses `rmlint` to identify and remove duplicate files.

3. **Rename Files**: Renames all files using the `ren` command (specifics depend on your `ren` configuration).

4. **Remove Metadata (First Pass)**: Strips all metadata from files using `exiftool`.

5. **Remove Small Files**: Deletes all files smaller than 100KB.

6. **Convert WEBP Files**: 
   - Converts WEBP files to PNG.
   - If a WEBP file is actually a GIF, it's converted to GIF format.

7. **Convert Small JPGs to PNG**: Converts JPG files smaller than 1MiB to PNG format.

8. **Remove Metadata (Second Pass)**: Another round of metadata removal.

9. **Remove Duplicates (Second Pass)**: Another round of duplicate removal using `rmlint`.

10. **Remove Larger Small Files**: Deletes all files smaller than 1MiB.

## Usage

1. Place the script in the directory containing the files you want to process.
2. Make the script executable:
   ```
   chmod +x script_name.sh
   ```
3. Run the script:
   ```
   ./script_name.sh
   ```

## Caution

- This script performs destructive operations. It will permanently delete files and modify others.
- Always back up your data before running this script.
- Review and understand each operation before executing the script.

## Customization

You can modify the script to adjust:
- File size thresholds for deletion
- Image conversion parameters
- Specific file types to process or ignore

## Notes

- The script provides progress updates for each major operation.
- Some operations are performed twice (e.g., metadata removal, duplicate removal) for thoroughness.
- The effectiveness of the script depends on the accuracy and functionality of the external tools it uses.

## Troubleshooting

If you encounter issues:
1. Ensure all required tools are installed and up-to-date.
2. Check file permissions in the directory.
3. Review the output for any error messages from individual commands.
