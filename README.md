# DeepRadio - Terminal Radio Station

A simple, minimal terminal-based radio player with automatic station installation and dynamic menu generation. Listen to your favorite radio stations from any system with a clean command-line interface.

## 🎵 Features

- **Automatic Station Installation**: Downloads and installs radio stations automatically
- **Dynamic Menu**: Menu adapts based on available stations
- **Cross-Platform**: Works on Linux, macOS, and other Unix-like systems
- **Smart Installation**: Only downloads missing stations, skips already installed ones
- **Automatic mpv Installation**: Detects and installs mpv player automatically
- **Configurable Stations**: Easy to add new stations via configuration file
- **Error Handling**: Robust error handling with timeout and connection checks

## 🚀 Quick Start

```shell
# Make scripts executable
chmod +x radio install-stations install-deps

# Install dependencies (mpv and curl)
./install-deps

# Run the radio player (installs stations automatically)
./radio
```

## 📁 Project Structure

```
deepradio/
├── radio                 # Main radio player script
├── install-stations      # Station installation script
├── install-deps          # Dependencies installer (mpv, curl)
├── stations/
│   ├── stations.conf     # Station configuration file
│   ├── *.ogg.m3u        # Radio station playlist files
│   └── README.md        # Station-specific documentation
└── README.md            # This file
```

## ⚙️ Configuration

### Adding New Stations

Edit `stations/stations.conf` to add new radio stations:

```bash
# Format: station_name|display_name|url|needs_referer
station_name|Display Name|http://example.com/stream.m3u|true
```

**Parameters:**
- `station_name`: Internal name (used for filename)
- `display_name`: Name shown in menu
- `url`: Stream URL
- `needs_referer`: `true` for HBR1 stations, `false` for others

### Example Configuration

```bash
# HBR1 stations (require referer)
trance|Trance|http://www.hbr1.com/playlist/trance.ogg.m3u|true
ambient|Ambient|http://www.hbr1.com/playlist/ambient.ogg.m3u|true
tronic|Tronic|http://www.hbr1.com/playlist/tronic.ogg.m3u|true

# Other stations (no referer needed)
dubstepfm|Dubstep|www.dubstep.fm/listen.m3u|false
srf1|SRF 1|http://stream.srg-ssr.ch/drs1/mp3_128.m3u|false
srf2|SRF 2|http://stream.srg-ssr.ch/drs2/mp3_128.m3u|false
```

## 🎮 Usage

### Basic Usage

```shell
./radio
```

The script will:
1. Check if dependencies (mpv, curl) are installed
2. Install missing radio stations
3. Display dynamic menu with available stations
4. Play selected station

### Manual Dependencies Installation

```shell
./install-deps
```

Install mpv and curl dependencies automatically.

### Manual Station Installation

```shell
./install-stations
```

Manually install/update stations without starting the player.

## 🛠️ Requirements

- **mpv**: Media player (installed automatically)
- **curl**: For downloading station playlists
- **bash**: Shell environment
- **Internet connection**: For downloading stations

## 🔧 Installation

### Automatic Installation

The script automatically detects your system and installs mpv:

- **Ubuntu/Debian**: `sudo apt install mpv`
- **Fedora/RHEL**: `sudo dnf install mpv`
- **Arch Linux**: `sudo pacman -S mpv`
- **macOS**: `brew install mpv`

### Manual Installation

If automatic installation fails, install mpv manually:

```bash
# Ubuntu/Debian
sudo apt install mpv

# Fedora/RHEL
sudo dnf install mpv

# Arch Linux
sudo pacman -S mpv

# macOS
brew install mpv
```

## 🎯 How It Works

1. **Station Detection**: Reads `stations/stations.conf` for station definitions
2. **Installation Check**: Verifies which stations are already installed
3. **Download**: Downloads missing station playlists using curl
4. **Menu Generation**: Builds dynamic menu based on available stations
5. **Playback**: Uses mpv to play selected radio streams

## 🐛 Troubleshooting

### Common Issues

**"mpv is not installed"**
- The script will offer to install mpv automatically
- If that fails, install mpv manually using your package manager

**"No stations available"**
- Check your internet connection
- Verify station URLs in `stations/stations.conf`
- Check if station servers are accessible

**"Failed to install [station]"**
- Station server might be down
- URL might be incorrect
- Network timeout (script waits 30 seconds)

### Debug Mode

To see detailed installation process:

```bash
# Run with verbose output
bash -x ./install-stations
```

## 📝 Customization

### Adding Custom Stations

1. Edit `stations/stations.conf`
2. Add your station in the format: `name|Display|URL|referer_flag`
3. Run `./radio` - new station will be automatically installed

### Modifying Installation Behavior

Edit `install-stations` to:
- Change timeout values (`--connect-timeout`, `--max-time`)
- Modify user agent string
- Add custom headers

## 🤝 Contributing

Feel free to:
- Add new radio stations to `stations.conf`
- Improve error handling
- Add new features
- Report bugs

## 📄 License

This project is open source. Feel free to use and modify as needed.

## 🙏 Acknowledgments

- HBR1 for providing excellent radio streams
- Dubstep.fm for their streaming service
- The open source community for mpv and other tools

---

**Enjoy your music!** 🎵
