# abs-wear

**Status:** 🚧 In Entwicklung — Phase 1 MVP merged
**Repo:** https://github.com/severanceremus-cloud/abs-wear
**Collaborator:** scrato (Admin)
**Zuletzt aktualisiert:** 2026-03-24

## Was ist das?

Audiobookshelf WearOS Client mit Companion Phone App. Erlaubt das Hören von Hörbüchern direkt auf der Wear-Uhr — Auth über die Phone App.

## Module

### 📱 Phone App (`de.scrato.abswear.phone`)
- OAuth2 PKCE Login via Authentik OIDC
- Username/Password Fallback
- Token-Management mit verschlüsseltem DataStore (EncryptedSharedPreferences)
- Token-Sync zur Watch via Wear Data Layer
- Background Token Refresh via WorkManager

### ⌚ WearOS App (`de.scrato.abswear.wear`)
- Token-Empfang via `WearableListenerService`
- Bibliotheks-Browse mit `ScalingLazyColumn`
- Buchdetail-Screen mit Fortschrittsanzeige
- Media3 ExoPlayer Playback Service
- Progress-Sync alle 30 Sekunden
- Play/Pause und Skip-Controls

### 🔧 Shared Module (`de.scrato.abswear.shared`)
- Retrofit API-Interfaces für ABS (`AbsApiService`, `AbsAuthService`)
- DTOs für alle API-Responses
- `TokenManager` Interface
- Data Layer Message Paths

## Roadmap

- [x] Phase 1: MVP — Basis-Auth, Library-Browse, Playback
- [ ] Phase 2: Offline-Caching, Playlist-Support
- [ ] Phase 3: Complications, Tiles

## PRs

- [PR #1](https://github.com/severanceremus-cloud/abs-wear/pull/1) — Phase 1 MVP ✅ merged (2026-03-24)

## Tech Stack

- Kotlin, Jetpack Compose (Phone + Wear)
- Media3 / ExoPlayer
- Retrofit2 + OkHttp
- Hilt (DI)
- Gradle Version Catalogs (`libs.versions.toml`)

## Verknüpfungen

- [[myarchivist]] — unabhängig, gleiches Ökosystem
- [[ts3-listener]] — unabhängig
