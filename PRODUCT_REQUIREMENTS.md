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

## Non-Functional
- Fast performance
- Secure credential handling
- Offline schedule cache

## Tech
- Flutter + flutter-tvos
- State: Riverpod
- API: Free sports data

## Milestones
1. Basic dashboard + scores
2. IPTV player
3. Matching logic
4. Polish & deploy