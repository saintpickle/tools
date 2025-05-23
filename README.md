# Tools

A collection of utility scripts for macOS to help with various development and system tasks.

## Repository Description

This repository contains various command-line tools and utility scripts designed to enhance productivity on macOS. Currently, it includes:

- **iconsetgen**: A utility script for generating different sized icons and .icns files for macOS applications (only works on MacOS)
- **img2svg**: A utility script for converting raster images (PNG, JPEG, BMP, TIFF) to SVG vector format

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
| icon_48x48.png         | 48x48       | Standard size                  |
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
| icon.ico               | -           | Windows icon resource file     |

#### How it Works:

The script:
1. Creates a temporary directory `icons.iconset`
2. Uses `sips` to generate all required icon sizes
3. Uses `iconutil` to convert the iconset to an .icns file
4. Copies all generated icons to the current directory
5. Cleans up the temporary directory

For best results, use a high-resolution square PNG image (at least 1024x1024) as your source image.

### img2svg

`img2svg` is a utility script that converts raster images to SVG vector format. This tool supports multiple image formats and can process individual files or entire directories.

#### Usage:

1. For a single file:
```bash
img2svg image.png                 # Converts to image.svg
img2svg photo.jpg custom.svg      # Converts to custom.svg
```

2. For a directory of images:
```bash
img2svg images/                   # Converts all supported images in the directory
img2svg images/ output_dir/       # Converts all images to the output directory
```

3. Get help:
```bash
img2svg --help
```

#### Supported Formats:

- PNG
- JPEG/JPG
- BMP
- TIFF/TIF

#### Requirements:

- macOS with Homebrew
- The script will automatically offer to install required dependencies:
  - ImageMagick (for image processing)
  - Potrace (for bitmap tracing)

#### How it Works:

The script:
1. Checks for required dependencies and offers to install them
2. Processes the input image with ImageMagick to prepare it for tracing
3. Uses Potrace to convert the bitmap to vector SVG format
4. Outputs the resulting SVG file(s)

### gh-tool

`gh-tool` is a GitHub utility tool that simplifies common GitHub operations, particularly focused on making pull request workflows more intuitive and efficient.

#### Usage:

1. Checkout a pull request:
```bash
gh-tool pr checkout 123       # Fetches and checks out PR #123 to a local branch
```

2. View pull request information:
```bash
gh-tool pr info 123           # Display metadata about PR #123
```

3. Check status of pull requests:
```bash
gh-tool pr status             # Show status of open PRs for the repository
```

4. Clean up pull request branches:
```bash
gh-tool pr cleanup 123        # Cleanup the branch for PR #123
gh-tool pr cleanup            # Cleanup all merged PR branches
```

5. Manage configuration:
```bash
gh-tool config set default_remote upstream  # Change the default Git remote
gh-tool config get github_token             # View your GitHub token
```

6. Get help:
```bash
gh-tool --help                # Show general help
gh-tool pr --help             # Show help for PR commands
```

#### Features:

- **Simplified PR Checkout**: Replaces complex commands like `git fetch origin pull/ID/head:BRANCHNAME` with a more intuitive syntax
- **Configuration Management**: Persistent configuration for GitHub operations
- **Colorized Output**: Clear, color-coded feedback for better readability
- **Repository Validation**: Automatic checks to ensure you're in a valid Git repository
- **Extensible Design**: Easy to add new GitHub-related operations

#### Requirements:

- Python 3.6 or higher
- Git command-line tools
- A GitHub account and repository access

#### Configuration:

The tool stores configuration in `~/.gh-tool/config.json` with these default settings:

| Setting         | Default | Description                                  |
|-----------------|---------|----------------------------------------------|
| default_remote  | origin  | The Git remote to use for operations         |
| url_type        | https   | URL type (https or ssh) for GitHub URLs      |
| github_token    |         | Optional GitHub token for API operations     |

You can customize these settings using the config commands:

```bash
gh-tool config set default_remote upstream
gh-tool config set url_type ssh
```

The conversion process uses bitmap tracing to create vector outlines from the raster images. For best results, use images with:

- High contrast
- Clean, distinct edges
- Limited noise or grain
- Simple designs (complex photos may produce large SVG files with many paths)

This tool is particularly useful for converting logos, icons, and simple illustrations to scalable vector format.
