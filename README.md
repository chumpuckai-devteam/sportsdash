# SportsDash (Flutter prototype)

Cross-platform **sports IPTV player** with a live scores dashboard.  
Built with Flutter + Riverpod. Inspired by Scorebox-style scoreboards, focused on watching the game.

> **Native Apple app:** production iOS/tvOS work lives in  
> **[sportsdash-apple](https://github.com/chumpuckai-devteam/sportsdash-apple)** (SwiftUI).  
> This Flutter repo is kept as the reference prototype.

## Features

| Area | What you get |
|------|----------------|
| **Dashboard** | Today’s live / upcoming / final games, league filters, favorites, score ticker |
| **Scores API** | Free ESPN public scoreboards — major football, basketball, baseball, hockey, soccer, tennis, golf, racing, UFC, rugby (when available) — no API key |
| **Offline cache** | Last schedule cached for offline viewing |
| **IPTV** | M3U playlist URL or Xtream Codes credentials |
| **Guide** | TV guide grid by provider group; EPG via Xtream short EPG or M3U XMLTV (`url-tvg`) |
| **Matching** | Auto-match games → channels via teams, league, and broadcast networks |
| **Player** | **media_kit** (libmpv); LIVE jump, aspect cycle, HW/SW decoder in Settings; scores strip + stream picker |
| **Security** | Xtream password via `flutter_secure_storage` (with prefs fallback) |
| **UI** | Dark broadcast-booth theme (gold / live cyan) |

## Platforms

- **macOS** — local desktop testing (`flutter run -d macos`)
- **iOS** — Simulator or device (primary IPTV target with Android)
- **Android** — emulator or device
- **Web** — UI/scoreboard (`flutter run -d chrome`; video limited)
- **Apple TV (tvOS)** — **not** first-class Flutter; needs a special toolchain later

## Getting started

```bash
flutter pub get
flutter run -d macos
```

### iOS (Simulator)

```bash
open -a Simulator
cd ios && pod install && cd ..
flutter devices
flutter run -d ios
# or: flutter run -d <simulator-id>
```

Physical iPhone: open `ios/Runner.xcworkspace` → **Signing & Capabilities** → choose your Team, then `flutter run -d <device-id>`.

### Android

```bash
flutter run -d android
```

### Apple TV

Stock Flutter has no production tvOS target. Plan phone iOS + Android first; tvOS is a separate milestone (flutter-tvos / native shell).

### First run

1. **Scores** tab loads live ESPN scoreboards automatically.
2. **Channels** ships with demo MP4 streams so the player works without a provider.
3. **Settings** → IPTV source + **Player** (decoder / aspect).
4. Open a game → **Watch** → use **LIVE** if delayed, aspect icon to cycle fit, scores strip to switch games.

## Project layout

```
lib/
  main.dart
  theme/app_theme.dart
  models/          # Game, IptvChannel, IptvConfig
  services/        # SportsApi, IptvService, MatchingService, StorageService
  providers/       # Riverpod state
  screens/         # Dashboard, Channels, Player, Settings
  widgets/         # GameCard, LiveBadge, LiveScoresStrip
```

## Milestones (from PRD)

1. ✅ Basic dashboard + scores  
2. ✅ IPTV player (M3U / Xtream + demo streams)  
3. ✅ Matching logic  
4. ⬜ Polish & deploy (notifications, PIP/casting, full EPG, TV remote focus)

## Notes

- ESPN endpoints are public and unofficial; treat them as best-effort.
- HLS/TS IPTV feeds may need a more specialized player on some platforms; demo MP4s validate the pipeline.
- Use only playlists / credentials you are authorized to use.

## License

Private / unpublished (`publish_to: none`).
