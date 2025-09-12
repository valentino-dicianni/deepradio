# DeepRadio Stations Directory

This directory contains radio station configuration and playlist files for DeepRadio.

## 📁 Contents

- `stations.conf` - Station configuration file
- `*.ogg.m3u` - Radio station playlist files
- `README.md` - This documentation

## ⚙️ Adding New Stations

### Method 1: Edit Configuration File

1. Open `stations.conf` in a text editor
2. Add your station in the format:
   ```
   station_name|Display Name|http://example.com/stream.m3u|needs_referer
   ```
3. Run `./radio` - the station will be automatically installed

### Method 2: Manual Discovery

To find new radio stations:

1. **Open browser** and navigate to the radio station's website
2. **Inspect element** (F12) and look for audio/stream elements
3. **Find the .m3u URL** in the network tab or page source
4. **Test with curl**:
   ```bash
   curl -X GET "http://station-url.m3u" -H "User-Agent: Mozilla/5.0..."
   ```
5. **Add to stations.conf** following the format above

### Configuration Format

```
station_name|Display Name|URL|needs_referer
```

**Parameters:**
- `station_name`: Internal name (used for filename)
- `display_name`: Name shown in radio menu
- `url`: Direct stream URL (.m3u file)
- `needs_referer`: `true` for HBR1 stations, `false` for others

### Examples

```bash
# HBR1 stations (require referer)
trance|Trance|http://www.hbr1.com/playlist/trance.ogg.m3u|true
ambient|Ambient|http://www.hbr1.com/playlist/ambient.ogg.m3u|true

# Other stations (no referer needed)
dubstepfm|Dubstep|www.dubstep.fm/listen.m3u|false
jazzfm|Jazz FM|http://jazz.example.com/stream.m3u|false
```

## 🔍 Finding Stream URLs

### Common Sources

1. **Radio Station Websites**: Look for "Listen Live" or "Stream" buttons
2. **Network Tab**: Monitor browser requests while playing audio
3. **Page Source**: Search for `.m3u`, `.pls`, or stream URLs
4. **Radio Directories**: Sites like shoutcast.com, icecast.org
5. **Curated Playlists**: [GitHub Gist with M3U playlists](https://gist.github.com/casaper/ddec35d21a0158628fccbab7876b7ef3) - Contains many public radio stations from:
   - 🇨🇭 **Switzerland (SRF)**: Public radio stations (SRF 1-4, Radio Swiss Classic, Radio Swiss Jazz)
   - 🇬🇧 **UK (BBC)**: BBC Radio 1-6, 1Xtra, World Service, Asian Network
   - 🇺🇸 **SomaFM**: Independent internet radio with various genres
   - 🇨🇭 **Swiss Private**: Non-commercial stations like Radio LoRa, Radio Stadtfilter

### Browser Developer Tools

1. **F12** → Network tab
2. **Play audio** on the website
3. **Look for requests** to `.m3u`, `.pls`, or audio files
4. **Copy the URL** and test with curl

### Testing URLs

```bash
# Test if a stream URL works
curl -I "http://example.com/stream.m3u"

# Download and inspect playlist
curl "http://example.com/stream.m3u" | head -10
```

## 📻 Using Curated Playlists

The [GitHub Gist](https://gist.github.com/casaper/ddec35d21a0158628fccbab7876b7ef3) contains ready-to-use M3U playlists with many radio stations. Here's how to use them:

### Extract Individual Stations

1. **Download a playlist** from the gist (e.g., `UK-BBC-Radio.m3u`)
2. **Open the file** and find stations you want
3. **Copy the stream URL** from the `#EXTINF` entries
4. **Add to stations.conf**:
   ```bash
   bbcradio1|BBC Radio 1|http://bbcmedia.ic.llnwd.net/stream/bbcmedia_radio1_mf_p|false
   ```

### Popular Stations from the Gist

**⚠️ Note**: Some URLs in the gist may be outdated. Always test URLs before adding them.

**Swiss Stations (Working):**
- SRF 1-4, Radio Swiss Classic/Jazz
- Radio LoRa, Radio Stadtfilter

**SomaFM Stations (Usually Working):**
- Groove Salad, Beat Blender, The Trip
- Mission Control, Dub Step Beyond

### Quick Test

```bash
# Test a Swiss station (working)
curl -s "http://stream.srg-ssr.ch/drs1/mp3_128.m3u" | head -1

# Test a SomaFM station (usually working)
curl -I "http://ice1.somafm.com/groovesalad-128-mp3"

# Test BBC station (likely outdated)
curl -I "http://bbcmedia.ic.llnwd.net/stream/bbcmedia_radio1_mf_p"

# Test a Swiss station  
curl -I "http://stream.srg-ssr.ch/drs1/mp3_128.m3u"
```

**Happy listening!** 🎵
