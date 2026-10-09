# Simple IPTV (Fire TV / Android TV)

A minimal IPTV player. It reads an M3U/M3U8 playlist and plays channels. No EPG, no extras.

## Remote control

| Button       | Action                                              |
|--------------|-----------------------------------------------------|
| UP           | Next channel                                        |
| DOWN         | Previous channel                                    |
| OK / Select  | Open the channel list (OK on a channel plays it)    |
| BACK         | Close the list / exit the app                       |
| MENU (≡)     | Load a new playlist                                 |

The playlist and the last watched channel are remembered between launches.

## Loading the playlist

On first launch you get two options:

1. **Choose file on this device** - opens the system file picker (needs a file manager
   app installed on the Fire TV, e.g. X-plore, since some Fire OS versions have no picker).
2. **Send from phone or computer** - the TV shows an address like `http://192.168.1.20:8080`.
   Open it in any browser on the same Wi-Fi, choose your .m3u file and tap Upload.

## Build the APK

1. Open this folder in **Android Studio** (Koala or newer) and let Gradle sync.
2. **Build > Build APK(s)**. Output: `app/build/outputs/apk/debug/app-debug.apk`
   (or from a terminal: `./gradlew assembleDebug`; if `gradlew` is missing run
   `gradle wrapper --gradle-version 8.9` once).

## Install on the Fire TV

1. Fire TV: Settings > My Fire TV > Developer Options > turn on **ADB debugging**
   and **Install unknown apps**.
2. On your computer: `adb connect <FIRE_TV_IP>:5555` then `adb install app-debug.apk`
3. The app appears in Your Apps & Channels (Apps > see all).

## Notes

- Works with HLS (.m3u8) and raw MPEG-TS/HTTP streams via ExoPlayer (Media3).
- Plain `http://` streams are allowed (most IPTV providers use them).
- Minimum Android version: 5.1 (API 22), i.e. every Fire TV Stick generation.
