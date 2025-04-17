# Tools

A collection of utility scripts for macOS to help with various development and system tasks.

## Repository Description

This repository contains various command-line tools and utility scripts designed to enhance productivity on macOS. Currently, it includes:

- **iconsetgen**: A utility script for generating different sized icons and .icns files for macOS applications (only works on MacOS)

## Installation Instructions

### 1. Clone the repository to your home directory

```bash
git clone https://github.com/saintpickle/tools.git ~/tools
```

### 2. Make the scripts executable

```bash
chmod +x ~/tools/*
```

### 3. Add the tools directory to your PATH

#### For zsh users (add to ~/.zshrc):

```bash
echo 'export PATH="$HOME/tools:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

#### For bash users (add to ~/.bashrc):

```bash
echo 'export PATH="$HOME/tools:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

## Tools

### iconsetgen

`iconsetgen` is a utility script that generates various icon sizes and an .icns file from a source PNG image. This is useful for creating icon sets for macOS applications.

#### Usage:

1. Place a source PNG image named `icon.png` in your current directory
2. Run the `iconsetgen` command
3. The script will generate all required icon sizes and an .icns file

```bash
cd path/to/your/project
iconsetgen
```

#### Requirements:
- macOS (uses the `sips` and `iconutil` commands)
- A source image named `icon.png` in the current directory

#### Generated Files:

The script generates the following files:

| File                   | Size        | Description                    |
|------------------------|-------------|--------------------------------|
| icon_16x16.png         | 16x16       | Standard size                  |
| icon_32x32.png         | 32x32       | Standard size                  |
| icon_64x64.png         | 64x64       | Standard size                  |
| icon_128x128.png       | 128x128     | Standard size                  |
| icon_256x256.png       | 256x256     | Standard size                  |
| icon_512x512.png       | 512x512     | Standard size                  |
| icon_16x16@2x.png      | 32x32       | Retina display (@2x)           |
| icon_32x32@2x.png      | 64x64       | Retina display (@2x)           |
| icon_64x64@2x.png      | 128x128     | Retina display (@2x)           |
| icon_128x128@2x.png    | 256x256     | Retina display (@2x)           |
| icon_256x256@2x.png    | 512x512     | Retina display (@2x)           |
| icon_512x512@2x.png    | 1024x1024   | Retina display (@2x)           |
| icon.icns              | -           | macOS icon resource file       |

#### How it Works:

The script:
1. Creates a temporary directory `icons.iconset`
2. Uses `sips` to generate all required icon sizes
3. Uses `iconutil` to convert the iconset to an .icns file
4. Copies all generated icons to the current directory
5. Cleans up the temporary directory

For best results, use a high-resolution square PNG image (at least 1024x1024) as your source image.
