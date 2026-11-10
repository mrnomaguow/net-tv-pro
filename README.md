# NetTV Pro

A live TV player and cloud DVR studio for your phone. Watch free live
streams, browse channels, check the programme guide, and schedule and
keep recordings — all in one app.

NetTV Pro is a single HTML app (`app/src/main/assets/www/index.html`)
wrapped in a small WebView shell, so the player you see in the app is
exactly the HTML in this repo.

## Features

- Live TV with HLS playback (hls.js)
- Preset free channels, plus search the public IPTV-org directory
  to find and add more stations
- Programme guide (EPG) for the current hour
- Scheduled recording and a DVR library (stored on your device
  with IndexedDB)
- Import your own channels from an M3U playlist
- Prev / Next channel buttons, in the player controls and in a bar
  under the video
- Real fullscreen video, with a fallback in the page itself
- Respects the status bar and navigation bar — no content hidden
  under the clock or the menu bar

## A note on streams

This app is only a player. The preset channels are other broadcasters'
free public streams (DW, France 24, NASA TV, Al Jazeera and others),
and the Find Stations search lists streams from the public IPTV-org
directory. Open-sourcing this code does not license those streams,
and some streams may not play in every browser: the app's WebView
allows file-URL access that desktop Chrome does not, so a stream
that plays in the app may be blocked by CORS in Chrome.

Recording a cross-origin stream can also save a black or silent
recording — the app warns about this instead of saving it silently.

## Building

Requires JDK 17 and the Android SDK (API 36, build-tools 36).

```sh
# point Gradle at your Android SDK, e.g.:
echo "sdk.dir=$HOME/Android/Sdk" > local.properties

./gradlew :app:assembleRelease
```

The release APK is unsigned — sign it with your own key, or let
F-Droid sign it.

## Project layout

- `app/src/main/assets/www/index.html` — the whole player app
- `app/src/main/java/com/livewire/MainActivity.java` — the WebView
  wrapper, with native fullscreen and safe-area margins
- `fastlane/metadata/` — F-Droid listing text and icon
- `fdroid/metadata/` — F-Droid build recipe (`com.livewire.nettvpro.yml`)

## License

Copyright 2026 Elijah Wougamon. Licensed under the Apache License,
Version 2.0. See [LICENSE](LICENSE).
