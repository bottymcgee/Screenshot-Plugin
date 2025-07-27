# Screenshot Plugin for HighLite

A plugin for the HighLite client that allows users to capture screenshots of the game window and save them to a local folder.

## Features

- **📸 Screenshot Button**: Click the camera icon in the titlebar to take a screenshot
- **🎵 Audio Feedback**: Hear a camera shutter sound when taking screenshots
- **Keyboard Shortcut**: Use `Ctrl+Shift+S` to quickly capture a screenshot
- **Dynamic Client Size Detection**: Automatically detects the current game window size
- **Customizable Settings**: Configure save directory, filename format, and timestamp options
- **Automatic File Organization**: Screenshots are saved to a dedicated subfolder
- **Unique Filenames**: Prevents overwriting with automatic filename incrementation
- **Real-time Feedback**: Success/error notifications when screenshots are saved

## Installation

The Screenshot plugin is distributed through the HighLite Plugin Hub and will be automatically installed when available.

## Usage

### Taking Screenshots

1. **Button Method**: Click the 📸 icon in the titlebar (next to the Discord button)
2. **Keyboard Shortcut**: Press `Ctrl+Shift+S` anywhere in the client

### Audio Feedback

When you click the screenshot button, you'll hear a quick camera shutter sound effect to confirm the action.

## Settings

### Enable Screenshot Plugin
- **Default**: Enabled
- **Description**: Toggle the entire screenshot plugin on/off

### Save Directory
- **Default**: `screenshots`
- **Description**: The subfolder where screenshots will be saved
- **Location**: `%APPDATA%/Highlite/screenshots/` (Windows) or equivalent

### Filename Format
- **Default**: `screenshot_{timestamp}_{count}`
- **Available Placeholders**:
  - `{timestamp}`: Date and time (if enabled)
  - `{count}`: Sequential screenshot number
- **Example**: `screenshot_2024-01-15_14-30-25_001.png`

### Include Timestamp
- **Default**: Enabled
- **Description**: Whether to include date/time in the filename

## File Structure

Screenshots are saved in the following structure:
```
%APPDATA%/Highlite/
└── screenshots/
    ├── screenshot_2024-01-15_14-30-25_001.png
    ├── screenshot_2024-01-15_14-30-25_002.png
    └── ...
```

## Technical Details

### Game Container Detection

The plugin automatically detects the game rendering area by looking for:
1. Canvas elements (most common for games)
2. Game-specific containers (`#game-container`, `.game-container`, etc.)
3. Main content areas (`#body-container`, `main`, etc.)
4. Falls back to the entire document body if no specific container is found

### Screenshot Process

1. **Detection**: Identifies the game container and its current dimensions
2. **Audio Feedback**: Plays a camera shutter sound effect
3. **Capture**: Uses Electron's `webContents.capturePage()` to capture the specific area
4. **Processing**: Converts to PNG format (lossless)
5. **Filename Generation**: Creates unique filename with automatic incrementation
6. **Saving**: Writes the file to the configured directory
7. **Feedback**: Shows success/error notification to the user

### Unique Filename System

The plugin ensures no files are overwritten by:
- Checking for existing files in the filesystem
- Adding `_1`, `_2`, etc. to filenames when duplicates exist
- Tracking used filenames during the current session

## Development

### Prerequisites

- Node.js (v22 or higher recommended)
- Yarn package manager (v1.22.22 or compatible)

### Building

```bash
# Install dependencies
yarn install

# Build for production
yarn build

# Development mode with file watching
yarn dev
```

### Local Testing

1. Build the plugin: `yarn build`
2. Copy `dist/ScreenshotPlugin.js` to your HighLite plugins directory
3. Restart HighLite to load the plugin

## License

This project is licensed under the terms specified in the LICENSE file.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Support

For support, please create an issue in this repository or reach out on Discord. 