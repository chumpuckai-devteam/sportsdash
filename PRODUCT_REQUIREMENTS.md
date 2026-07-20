# Product Requirements Document (PRD) - SportsDash

## Overview
Cross-platform sports-focused IPTV player with live scores dashboard.
Inspired by Scorebox but customized.

## Target Platforms
- iOS & tvOS (Apple TV)
- Android & Android TV
- Web (for quick testing)

## Core Features
1. **Dashboard**
   - Today's live/upcoming games
   - Real-time scores
   - League filters, favorites
2. **IPTV Integration**
   - M3U/Xtream Codes support
   - Channel list with search
   - Auto-match games to streams
3. **Player**
   - Fullscreen with score overlay
   - Controls, PIP, casting
4. **Additional**
   - Notifications for game starts/goals
   - Dark sports UI
   - EPG where available
5. **Movie ratings on now-playing channels** *(new)*
   - When an IPTV channel’s current program is a **movie** (from EPG/guide metadata, or clear movie title signals), show **audience/critic-style ratings** similar to Rotten Tomatoes (e.g. Tomatometer + audience score, or equivalent certified aggregate scores).
   - Surfaces (minimum):
     - Channel list / guide row for the now-playing title
     - Player chrome or info overlay while watching
     - Optional: game/channel detail sheet when the matched content is a film
   - Resolve ratings by matching the now-playing title (+ year if available) to a movie metadata provider; prefer open or licensed APIs (e.g. TMDB + linked rating sources, OMDb, or a Rotten Tomatoes–class feed if licensed).
   - Graceful degradation: if the program is not a movie, or no confident match / no score, hide the rating UI (no fake scores).
   - Cache ratings offline for recently seen titles; refresh on a reasonable TTL.
   - Do not block stream playback on ratings fetch.

## Non-Functional
- Fast performance
- Secure credential handling
- Offline schedule cache
- Ratings lookups must be non-blocking and rate-limit safe

## Tech
- Flutter + flutter-tvos (prototype / reference)
- Native Apple: SwiftUI (`sportsdash-apple`)
- State: Riverpod (Flutter) / AppModel (Apple)
- API: Free sports data (ESPN public scoreboards)
- Movie ratings: TBD metadata provider (see requirement 5)

## Acceptance criteria (movie ratings)
- [ ] Given EPG (or equivalent) marks now-playing as a movie with a title, the UI shows at least one recognizable quality score (critic and/or audience).
- [ ] Given a live sports or non-movie program, no movie-rating chrome appears.
- [ ] Given an unmatched or ambiguous title, UI omits ratings rather than guessing.
- [ ] Opening a stream does not wait on the ratings network call.
- [ ] Scores remain visible/readable on dark broadcast UI (contrast).

## Milestones
1. Basic dashboard + scores
2. IPTV player
3. Matching logic
4. Polish & deploy
5. **Movie ratings for now-playing IPTV movies** (guide + player)
