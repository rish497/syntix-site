# Syntix Privacy Policy — draft

Developer/operator: Rishabh Mittal
Contact email: mittal.rishabh2010@gmail.com
Proposed effective date: 3 November 2026 (subject to actual publication)
Last updated: 3 November 2026 (draft; not legal approval)
Operator location: Indirapuram, Ghaziabad, Uttar Pradesh, India
Intended release regions: worldwide
Planned distribution: Uptodown and Aptoide

## Scope

This policy describes the Android app inspected for this draft. It does not cover the repository's separate browser extension, development preview servers, or the independent practices of YouTube, Google, Spotify, GitHub or document providers. The current app has local profiles, not a developer-operated online account or cloud-sync service. No developer-operated backend, analytics, advertising SDK or automatic crash-upload integration was identified in the inspected Android implementation. This does not mean that no data is processed or that no information leaves the device.

## Information stored locally

Syntix stores profile names, random local profile IDs, the active profile and references to user-selected profile photos. Profiles are not password-protected. Someone who can open Syntix on your unlocked phone can switch between them. Profile separation is a convenience, not an authentication or encryption boundary.

Local app data also includes playlists and their names, media titles, artist/channel names, URLs, thumbnails, durations, Favorites, imported-video references, the listening queue, shuffle/repeat state, import progress, listening history, play counts and listening timestamps. Recommendations and Smart Mixes use this history. The retained history is not limited to three months.

Statistics record listening time, artist/channel listening totals, app network-byte observations and observed battery-level changes. Statistics older than the last three calendar months are pruned when the statistics database is maintained. Battery observations are not a precise measurement of energy attributable only to Syntix.

Preferences include a local record of Terms acceptance/privacy acknowledgement (document version and timestamp), onboarding state, library layout, sound/equalizer and sleep-timer options, download quality, Wi-Fi-only downloading and download progress/indexes. Public search-result metadata is cached in app files with a bounded index and seven-day freshness limit. A shared, device-local Spotify recording-match cache holds up to 512 matches for seven days; it is not isolated by profile. Expired caches are not a promise of immediate physical erasure from storage. Artwork uses memory and an approximately 8 MiB HTTP disk cache. The extraction engine, its version/update information and supporting runtime files are also stored locally.

Offline audio is stored in private app files, separated by profile. Audio/MP4 exports are written to the destination you choose. Local audio and profile-photo selections retain document-provider URI references/access grants; Syntix does not need to upload a profile photo to display it. Temporary export files are created in app cache and deletion is attempted when the operation finishes. Errors may be written to Android's local system logs; no automatic developer log-upload path was identified.

## Information sent to external services

- YouTube/Google receive search terms, autocomplete text, video and playlist identifiers/URLs, and requests needed to retrieve metadata or media. Recommendation searches can include song titles and channels derived from your local listening history. Spotify-to-YouTube matching sends the source song's title and artist as YouTube search queries.
- Google autocomplete is requested from `suggestqueries.google.com/complete/search`. YouTube search uses `www.youtube.com/results` and `www.youtube.com/youtubei/v1/search`. The latter is an internal web-client endpoint, not a configured YouTube Data API project.
- YouTube playback, downloads and exports use yt-dlp through youtubedl-android and media requests to URLs returned by that engine, including YouTube/Google media hosts such as subdomains of `googlevideo.com`. YouTube page/player/script endpoints and redirects can vary with the upstream engine.
- Spotify playlist import requests public pages at `open.spotify.com/embed/playlist/{id}` and `open.spotify.com/playlist/{id}`. The inspected import does not sign into Spotify or retrieve Spotify audio.
- Artwork requests go to `i.ytimg.com` or another HTTPS image URL supplied in media metadata. Those URLs and any subsequent redirects determine the image host actually contacted.
- The implemented stable playback-engine update action checks `api.github.com/repos/yt-dlp/yt-dlp/releases/latest` and downloads an upstream release asset via GitHub and its delivery hosts. It does not upload your library. The action remains in the legacy Settings code, which currently has no normal Settings navigation entry.

These services and network intermediaries can receive your IP address, the requested URL/query, timing and ordinary HTTP/client metadata. The extractor may send browser, language or device-like client fields required by its upstream requests. This audit did not identify an app-upload path for the local profile name/photo, complete local library, statistics database, advertising ID or a hardware device identifier. Requests still reveal the content you search for or play. Third parties may associate requests with information they independently hold and apply their own retention and privacy rules. Syntix cannot delete their records.

A new-profile checkbox records Terms acceptance and acknowledgement of this policy locally. It is not a parental-consent mechanism or a claim that all processing is based on consent. Existing profiles are not blocked by a new startup acceptance screen.

Selecting a file provider or sharing/exporting a file can involve other apps or cloud storage chosen by you. Exported content and backups may therefore leave the physical device through that provider. Syntix's use of the Android file picker is not a guarantee that the destination is local-only.

## Permissions and device access

- INTERNET and ACCESS_NETWORK_STATE: retrieve metadata, artwork, media and engine updates; observe connectivity, including Wi-Fi-only download preferences.
- WAKE_LOCK: support media playback without the CPU sleeping mid-playback.
- FOREGROUND_SERVICE and FOREGROUND_SERVICE_MEDIA_PLAYBACK: ongoing playback with Android media controls.
- FOREGROUND_SERVICE_DATA_SYNC: foreground offline-download and file-export work.
- POST_NOTIFICATIONS: media/download status and controls, subject to Android notification permission settings.
- AndroidX adds an app-specific, signature-protected dynamic-receiver permission in the merged manifest; it is not an additional user-data permission.

The inspected manifest requests no microphone, camera, contacts, location, Accessibility, overlay or broad shared-storage permission. Photos/audio/export destinations are selected through Android's document picker. System notifications and media controls can show track names/artwork on your lock screen, depending on your Android settings.

## Deleting information and controlling storage

Use playlist options to delete a saved playlist, song actions to remove a song or imported-video entry, and the heart control to remove a Favorite. In an offline-download management sheet, the existing Remove downloaded audio action removes the active profile's managed offline files and pending downloads. It does not delete playlists, Favorites or separately exported files.

A Clear listening history action exists in the legacy Settings/history sheet and also clears the active profile's statistics and recommendations. That Settings entry is not exposed by the current normal navigation; this policy does not claim a new deletion control has been added. There is no current per-profile delete-account action or single in-app wipe-everything control.

To remove all private Syntix data, use Android Settings, Apps, Syntix, Storage, Clear storage/Clear data, or uninstall the app. Android wording varies by phone. Remove exported audio/MP4/backup files separately in the destination file manager or cloud provider. External services' records, other apps' copies and already shared files are not removed by clearing Syntix storage. Android controls device access grants and some residual system records.

## Backup and security limits

The manifest sets `allowBackup=false` and defines no `dataExtractionRules` or `fullBackupContent` rules. No developer cloud backup/sync is configured. Android/OEM device-transfer behavior can vary; this is not a guarantee that every device-transfer mechanism is disabled. Private preferences/files and the SQLite database use Android app storage protections, without app-level profile passwords or a separate app-managed encryption layer identified in this audit. Keep the phone itself secured.

## Children

Syntix is intended for people aged 13 and older (13+), and is not intended for children under 13. By creating a local profile, you confirm you are at least 13. If local law or an external service requires a higher age or a parent/guardian's permission, those requirements also apply. The app records your acknowledgement locally; it does not verify your age or provide a verified parental-consent mechanism. If you believe information about a child under 13 requires attention, contact mittal.rishabh2010@gmail.com. A 13+ minimum is not a certification of worldwide children's-privacy compliance or a store content rating.

## Questions and changes

Contact mittal.rishabh2010@gmail.com with privacy questions. Include only information needed to explain your request; do not send account passwords or tokens. Future changes to the app's data handling require updating this policy and its effective date. This draft must be completed and reviewed before public publication.
