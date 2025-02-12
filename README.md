# Make Your Own Super Wallpaper

Create stunning, customized Super Wallpapers by modifying Xiaomi's Super Wallpaper APK. This guide provides two methods to achieve fully customizable Super Wallpapers that work on any Android device.

## Table of Contents

- [Features](#features)
- [Methods](#methods)
  - [Option 1: Easy Method](#option-1-easy-method)
  - [Option 2: Advanced Method](#option-2-advanced-method)
- [Requirements](#requirements)
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

1. Download the Miside Super Wallpaper APK
2. Decompile using APKTool:
   ```bash
   apktool d miside_super_wallpaper.apk -o miside_decompiled
   ```
3. Navigate to the video file location in the decompiled folder
4. Replace with your custom MP4 video (maintain original filename)
5. Recompile and sign:
   ```bash
   apktool b miside_decompiled -o modified.apk
   java -jar signapk.jar certificate.pem key.pk8 modified.apk signed.apk
   ```
6. Install and apply the modified wallpaper

### Option 2: Advanced Method

For users comfortable with 3D asset modification, this method enables customization of the Moon Super Wallpaper's 3D objects.

1. Obtain the ported version of Xiaomi Moon Super Wallpaper
2. Decompile the APK:
   ```bash
   apktool d moon_super_wallpaper.apk -o moon_decompiled
   ```
3. Locate and modify texture files in the assets folder
4. Follow the same recompilation and signing process as Option 1
5. Install and apply the modified wallpaper

## Requirements

### Software
- APKTool (version 2.7.0 dirty or 2.10.0 dirty is recommend)
- Android devices
- Basic linux / windows command-line knowledge

## Troubleshooting

If you encounter issues:

1. Verify all required tools are properly installed
2. Double-check file permissions
3. Ensure original filenames are preserved
4. Validate texture file formats (for Option 2)

## License

This project is licensed under the GNU General Public License v3.0.

For complete license details, please refer to the [LICENSE](https://www.gnu.org/licenses/gpl-3.0.html) file.

---

**Note**: Always backup your original APK files before modification. The author is not responsible for any device damage resulting from improper modification. 