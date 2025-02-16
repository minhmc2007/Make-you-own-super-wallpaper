# Make Your Own Super Wallpaper

Create stunning, customized Super Wallpapers by modifying Xiaomi's Moon Super Wallpaper APK and S24 Infinity Wallpaper by Andro Radar. This guide provides two methods to achieve fully customizable Super Wallpapers that work on any Android device.

## Special thank to imDCStar and Ouxyl 

## Table of Contents

- [Features](#features)
- [Methods](#methods)
  - [Option 1: Easy Method](#option-1-easy-method)
  - [Option 2: Advanced Method](#option-2-advanced-method)
- [Requirements](#requirements)
- [Troubleshooting](#troubleshooting)
- [License](#license)

## Features

- Support for both 2D and 3D customization
- Cross-device compatibility (works on all Android devices)
- Two difficulty levels to choose from:
  - Beginner-friendly 2D video modification
  - Advanced 3D object customization

## Methods

### Option 1: Easy Method

This beginner-friendly approach allows you to replace the built-in video inside Miside Super Wallpaper.

1. Download the [Miside Super Wallpaper APK](https://objects.githubusercontent.com/github-production-release-asset-2e65be/916344626/ab5a8db1-9141-434a-84e0-794e34928dc1?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=releaseassetproduction%2F20250212%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20250212T143231Z&X-Amz-Expires=300&X-Amz-Signature=559860ccb6e40935aefee9e44230145af85805a0a14ccd917b5ca3987e635152&X-Amz-SignedHeaders=host&response-content-disposition=attachment%3B%20filename%3Dwallpaper.zip&response-content-type=application%2Foctet-stream)
2. Decompile using APKTool:
```bash
apktool d miside_super_wallpaper.apk -o miside_decompiled
```
3. Navigate to the video file location in the decompiled folder (assets folder)
4. Replace with your custom MP4 video (maintain original filename)
5. Recompile and sign:
```bash
apktool b miside_decompiled -o modified.apk --aapt2
java -jar signapk.jar certificate.pem key.pk8 modified.apk signed.apk
```
6. Install and apply the modified wallpaper
7. The fist frame in your video will be your lockscreen and the rest of video will be home screen.

### Option 2: Advanced Method

For users comfortable with 3D asset modification, this method enables customization of the Moon Super Wallpaper's 3D objects.

1. Obtain the ported version of Xiaomi Moon Super Wallpaper
2. Decompile the APK:
```bash
apktool d moon_super_wallpaper.apk -o moon_decompiled
```
3. Locate and modify texture files in the assets folder, inside texture-compressed and models (currently only texture editing is supported)
4. Use [KTX Tool](https://github.com/KhronosGroup/KTX-Software) to extract and pack textures. To extract all KTX files to PNG, use this script:
```bash
#!/bin/bash

# Check if required tools are installed
if ! command -v ktx2ktx2 &> /dev/null || ! command -v ktx extract &> /dev/null; then
    echo "Error: KTX-Software tools not found. Install them first."
    exit 1
fi

# Create output folder
mkdir -p extracted_pngs

# Function to process a single KTX file
convert_ktx_to_png() {
    local file="$1"
    local base_name="${file%.ktx}"  # Remove .ktx extension
    
    # Convert KTX1 to KTX2
    echo "Converting $file to KTX2..."
    ktx2ktx2 "$file"
    
    # Extract PNG from KTX2
    if [ -f "$base_name.ktx2" ]; then
        echo "Extracting PNG from $base_name.ktx2..."
        ktx extract "$base_name.ktx2" --output "extracted_pngs/$base_name.png"
        
        # Remove intermediate KTX2 file to save space
        rm "$base_name.ktx2"
    else
        echo "Error: KTX2 conversion failed for $file."
    fi
}

export -f convert_ktx_to_png  # Export function for parallel execution

# Find all .ktx files and process them in parallel
find . -maxdepth 1 -type f -name "*.ktx" | parallel -j "$(nproc)" convert_ktx_to_png

echo "Extraction complete. PNGs saved in 'extracted_pngs' folder."
```
5. To convert PNG back to KTX:
```bash
toktx input.png -o output.ktx
```
6. Follow the same recompilation and signing process as option 1
7. Install and apply the modified wallpaper

## Requirements

- APKTool (version 2.7.0 dirty or 2.10.0 dirty recommended)
- Android device
- Basic Linux/Windows command-line knowledge
- KTX Tool (Option 2 only)
- Java (for signing APK)

## Troubleshooting

1. Verify all required tools are properly installed
2. Ensure original filenames are preserved
3. Validate texture file formats (for Option 2)
4. If the app fails to compile, use [Android Reverse Engineer Framework](https://github.com/minhmc2007/Android-Reverse-Engineer-Framework) to patch the decompiled files
5. Use aapt2 only

## License

This project is licensed under the MIT License

---

**Note**: Always backup your original APK files before modification. The author is not responsible for any device damage resulting from improper modification. Only moon super wallpaper work with this tutorial.
