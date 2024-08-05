#!/bin/bash

echo "Unzipping and deleting zip files..."
unzip -B '*.zip'
rm *.zip
echo "Complete."

echo "Removing duplicates..."
rmlint
./rmlint.sh -d
rm rmlint.json
echo "Complete."

echo "Deleting files smaller than 100k..."
find . -maxdepth 1 -type f -size -100k -delete
echo "Complete."

echo "Striping extensions & renaming all files using 8 random digits..."
for file in *; do
if [ -f "$file" ]; then
	new_name=$(head /dev/urandom | base64 | tr -dc 0-9 | head -c8)
	while [ -e "$new_name" ]; do
		new_name=$(head /dev/urandom | base64 | tr -dc 0-9 | head -c8)
    done
mv -- "$file" "$new_name"
fi
done
echo "Complete."

echo "Getting file extensions from MIME types..."
get_extension() {
    local mime_type=$1
    case $mime_type in
        "image/gif") echo ".gif" ;;
        "image/jpeg") echo ".jpg" ;;
        "video/mp4") echo ".mp4" ;;
        "image/png") echo ".png" ;;
        "image/webp") echo ".webp" ;;
        # Add more MIME types and their corresponding extensions as needed
        *) echo "" ;; # Return empty if no match found
    esac
}
echo "Complete."

echo "Removing EXIF data..."
exiftool -all= -overwrite_original -r .
echo "Complete."

echo "Deleting files smaller than 100k again, prior to conversion, per removed exif data..."
find . -maxdepth 1 -type f -size -100k -delete
echo "Complete."

echo "Converting all .webp files to their respective formats..."
find . -type f -name "*.webp" -print0 | while IFS= read -r -d '' file; do
    # Check the file type
    file_type=$(identify -format "%m" "$file")
    case "$file_type" in
        WEBP)
            echo "Converting $file to PNG"
            magick "$file" "${file%.webp}.png"
            rm "$file"
            ;;
        GIF)
            echo "Converting $file to GIF"
            magick "$file" "${file%.webp}.gif"
            rm "$file"
            ;;
        *)
            echo "$file is not a WEBP file or is in an unexpected format, skipping."
            ;;
    esac
done
echo "Complete."

echo "Converting JPGs less than 1MiB to PNG..."
find . -type f -name "*.jpeg" -size -1000k -print0 | while IFS= read -r -d '' file; do
    mogrify -format png "$file"
    rm "$file"
done
echo "Complete."

# Remove EXIF data
echo "Removing EXIF data per newly-converted files..."
exiftool -all= -overwrite_original -r .
echo "Complete."

echo "Removing all files less than 1MiB..."
find . -type f -name '*.*' -size -2M -delete
echo "Complete."

echo "Cleaning up..."
# Function to delete contents of a directory
delete_contents() {
    local dir="$1"
    echo "Deleting contents of $dir"
    if [ -d "$dir" ]; then
        find "$dir" -mindepth 1 -delete 2>/dev/null
        echo "Contents of $dir have been deleted."
    else
        echo "Directory $dir does not exist."
    fi
}
# Delete contents of /home/u/.cache
delete_contents "/home/u/.cache"
# Delete contents of /home/u/.local/share/Trash
echo "Deleting contents of /home/u/.local/share/Trash"
if [ -d "/home/u/.local/share/Trash" ]; then
    rm -rf /home/u/.local/share/Trash/* 2>/dev/null
    echo "Contents of /home/u/.local/share/Trash have been deleted."
else
    echo "Directory /home/u/.local/share/Trash does not exist."
fi
echo "Complete."

echo "File processing complete."
