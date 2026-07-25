# Product Requirements Document (PRD) - SportsDash

## Overview
Sports-focused IPTV player with live scores dashboard.  
**Production client:** native **SwiftUI** on iOS (primary) and tvOS (`sportsdash-apple`).  
Flutter under `sportsdash/` is **reference / historical PRD only** — do not implement product features there.

Inspired by Scorebox-class sports IPTV apps, customized for multi-source playlists and a dark broadcast UI.

## Target platforms
| Platform | Status |
|----------|--------|
| **iOS** | Shipping / dogfood |
| **tvOS** | Target exists; focus polish parked |
| Android / Android TV | **Blocked** until Samir unblocks |
| Web | Not a product target |

## Design system (Apple-first)

SportsDash follows Apple HIG with **Liquid Glass** for the *navigation / control* layer only:

| Layer | Material | Examples |
|-------|----------|----------|
| **Navigation / controls** | Liquid Glass (`glassEffect`) on iOS 26+; `.ultraThinMaterial` fallback | Tab bar (system), category menus, filter chips, toolbar buttons |
| **Content** | Opaque elevated panels (`sportsContentCard`) | Game cards, channel tiles, guide rows, settings rows |
| **Canvas** | Void black (`SportsColors.voidBlack`) | Screen backgrounds — never full-screen glass |

**Do not** glass-fill lists, media, or full-screen content (HIG: Liquid Glass is for chrome that floats above content).

### Official references
- [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines)
- [Materials / Liquid Glass](https://developer.apple.com/design/human-interface-guidelines/materials)
- [Liquid Glass overview](https://developer.apple.com/documentation/technologyoverviews/liquid-glass)
- [Adopting Liquid Glass](https://developer.apple.com/documentation/technologyoverviews/adopting-liquid-glass)
- [SwiftUI](https://developer.apple.com/documentation/swiftui) — `Tab`, `Menu`, `glassEffect`, button styles
- In-repo: `sportsdash-apple/docs/ui-liquid-glass.md`, skill `references/apple-stack-map.md`

### Brand
- **App icon / splash:** SD monogram, gold + live mint on void black
- **Accent:** gold (`#FFB800`), live mint (`#00E5A0`)
- **Menus:** native SwiftUI `Menu` + `Picker` / sections (category, guide layout)

## Core features
1. **Scores dashboard** — live/upcoming games, league shelves, favorites, filters  
2. **IPTV** — M3U / Xtream, channel grid, search, categories  
3. **Guide** — EPG list/grid, category menu, movie rating chips  
4. **Player** — KSPlayer (default) + optional AVKit; floating mini-player; PiP; scores strip  
5. **Movie ratings** — OMDb primary → TMDB; Guide + player; never block playback  
6. **Settings** — playlists, general, UI, player, scores  

### Explicitly out of scope (parked)
- Multiview multi-stream (removed; blocked until explicit request)
- Android repo bootstrap (blocked)
- Game start / goal push notifications (blocked)
- Chromecast (not AirPlay; not built)
- VLC engine thrash mid-dogfood

## Non-functional
- Snappy UI: cache-first bootstrap; Guide category switch must not await EPG  
- Secure credentials (Keychain + verified fallback)  
- Offline channel + EPG cache  
- Ratings non-blocking and rate-limit safe  
- UI hierarchy: glass chrome ≠ content cards  

## Tech
| Layer | Choice |
|-------|--------|
| UI | SwiftUI (iOS 17+; Liquid Glass APIs when running iOS 26+) |
| State | `AppModel` |
| Player | **KSPlayer** (shipping default); AVKit optional |
| Scores | ESPN public scoreboards |
| Ratings | OMDb / TMDB |
| Project gen | XcodeGen (`Project.yml`) — **include** `Assets.xcassets` under sources (do not exclude `*.xcassets`) |

## Acceptance criteria — UI / Liquid Glass (Sprint UI)
- [ ] Tab bar uses modern `Tab` API on iOS 18+ (system Liquid Glass tab bar on iOS 26)  
- [ ] Filter chips / category menus use glass (or material fallback) — content cards stay opaque  
- [ ] Game cards, channel tiles readable on void background with clear LIVE/WATCH affordances  
- [ ] Settings is inset grouped list with AppLogo in About  
- [ ] No full-screen glass wash over video or guide content  
- [ ] Builds on iOS 17 SDK path without hard dependency failures (availability-gated glass)

## Acceptance criteria — movie ratings
- [x] Guide/player chips when movie + score available  
- [x] Hidden on sports / miss  
- [x] Playback never waits on ratings  

## Roadmap / milestones

| Phase | Focus | Status |
|-------|--------|--------|
| M1 | Scores + dashboard | Done |
| M2 | IPTV player + playlists | Done (KSPlayer) |
| M3 | Matching + guide EPG | Done |
| M4 | Movie ratings | Done (Sprint 1) |
| M5 | **Modern Apple UI** (Liquid Glass, menus, cards) | **In progress** |
| M6 | Performance polish (beyond cache-first) | Later — after UI |
| M7 | Player engine depth (AirPlay video, buffering UX) | Later — after UI |
| M8 | tvOS focus polish | Parked |
| M9 | Notifications | Parked |
| M10 | Android | Parked |

### Sprint UI (current)
1. Design tokens + `sportsGlass` / `sportsContentCard`  
2. Root tabs + Scores filters/cards  
3. Channels / Guide menus + cards  
4. Settings chrome  
5. Residual glass on player chrome (optional follow-up)  

## Kanban
Board: `sportsdash` · workdir `/opt/data/workspace/sportsdash-apple`  
Seed UI stories as shippable; keep Android/multiview/notifications **blocked**.
