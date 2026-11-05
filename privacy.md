# Syntix Privacy Policy — draft

Developer/operator: Rishabh Mittal
Contact email: mittal.rishabh2010@gmail.com
Proposed effective date: 3 November 2026 (subject to actual publication)
Last updated: 5 November 2026 (draft; not legal approval)
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

Completed offline audio is stored in per-profile private app files using AES-256-GCM authenticated encryption. Each file has its own random audio key, wrapped by an installation-local Android Keystore key. Playback decrypts authenticated chunks in memory to support seeking without creating a decrypted playback file. Existing indexed downloads are converted in the background or when first opened. Failed migrations retain the original and report that the download needs attention; encryption is not claimed complete until conversion succeeds. Download fragments and temporary transcoding files can contain plaintext in private app storage until completion. App encryption does not cover metadata, profiles, user-selected local audio, files saved by previous versions outside the app, or copies made by other apps. It is not service-authorized DRM and does not grant content rights. Clearing app data, uninstalling or losing the installation key can make saved encrypted audio unusable; download authorized content again if necessary.

Local audio and profile-photo selections retain document-provider URI references/access grants. Syntix does not need to upload a profile photo to display it. The current version does not offer standalone audio/video file exports. Errors may be written to Android's local system logs; no automatic developer log-upload path was identified.

## Information sent to external services

- YouTube/Google receive search terms, autocomplete text, video and playlist identifiers/URLs, and requests needed to retrieve metadata or media. Recommendation and public-playlist discovery searches can include song titles and channels derived from your local listening history. Public-playlist discovery metadata is cached per profile for freshness, and preset cartoon profile pictures are bundled in the APK. Spotify-to-YouTube matching sends the source song's title and artist as YouTube search queries.
- Google autocomplete is requested from `suggestqueries.google.com/complete/search`. YouTube search uses `www.youtube.com/results` and `www.youtube.com/youtubei/v1/search`, `/youtubei/v1/browse` for playlist metadata, and `/youtubei/v1/player` for public audio metadata. Recording matching also requests catalog song metadata from `music.youtube.com/youtubei/v1/search`. These are internal web-client endpoints, not a configured YouTube Data API project.
- YouTube playback and downloads use yt-dlp through youtubedl-android and media requests to URLs returned by that engine, including YouTube/Google media hosts such as subdomains of `googlevideo.com`. YouTube page/player/script endpoints and redirects can vary with the upstream engine. Native playback reuses anonymous visitor context supplied by YouTube, reused in memory with a 30-minute freshness window; it does not read Google account cookies. A small HTTP range request checks a returned public stream before use, without saving that probe as a download.
- Spotify song import requests public track metadata at `open.spotify.com/embed/track/{id}` and matches the title and artists to a YouTube recording; Spotify preview audio is not used. Spotify playlist import requests public pages at `open.spotify.com/embed/playlist/{id}` and `open.spotify.com/playlist/{id}`. Full-list pagination also requests an anonymous web session from `open.spotify.com/api/token` and public metadata from `api-partner.spotify.com/pathfinder/v1/query`. Public web-client configuration is requested from `code.thetadev.de/ThetaDev/spotify-secrets/`; that host receives the configuration-file request and ordinary connection information, not your playlist or song queries. The anonymous session is held in memory and is not a user Spotify login. The import does not retrieve Spotify audio.
- Artwork requests go to `i.ytimg.com` or another HTTPS image URL supplied in media metadata. Those URLs and any subsequent redirects determine the image host actually contacted.
- The implemented stable playback-engine update action checks `api.github.com/repos/yt-dlp/yt-dlp/releases/latest` and downloads an upstream release asset via GitHub and its delivery hosts. It does not upload your library. The action remains in the legacy Settings code, which currently has no normal Settings navigation entry.

These services and network intermediaries can receive your IP address, the requested URL/query, timing and ordinary HTTP/client metadata. The extractor may send browser, language or device-like client fields required by its upstream requests. This audit did not identify an app-upload path for the local profile name/photo, complete local library, statistics database, advertising ID or a hardware device identifier. Requests still reveal the content you search for or play. Third parties may associate requests with information they independently hold and apply their own retention and privacy rules. Syntix cannot delete their records.

A new-profile checkbox records Terms acceptance and acknowledgement of this policy locally. It is not a parental-consent mechanism or a claim that all processing is based on consent. Existing profiles are not blocked by a new startup acceptance screen.

Selecting a file provider or sharing a library backup or exporting application source can involve other apps or cloud storage chosen by you. Exported content and backups may therefore leave the physical device through that provider. Syntix's use of the Android file picker is not a guarantee that the destination is local-only.

## Permissions and device access

- INTERNET and ACCESS_NETWORK_STATE: retrieve metadata, artwork, media and engine updates; observe connectivity, including Wi-Fi-only download preferences.
- WAKE_LOCK: support media playback without the CPU sleeping mid-playback.
- FOREGROUND_SERVICE and FOREGROUND_SERVICE_MEDIA_PLAYBACK: ongoing playback with Android media controls.
- FOREGROUND_SERVICE_DATA_SYNC: foreground offline-download and conversion work.
- POST_NOTIFICATIONS: media/download status and controls, subject to Android notification permission settings.
- AndroidX adds an app-specific, signature-protected dynamic-receiver permission in the merged manifest; it is not an additional user-data permission.

The inspected manifest requests no microphone, camera, contacts, location, Accessibility, overlay or broad shared-storage permission. Photos/audio/export destinations are selected through Android's document picker. System notifications and media controls can show track names/artwork on your lock screen, depending on your Android settings.

## Deleting information and controlling storage

Use playlist options to delete a saved playlist, song actions to remove a song or imported-video entry, and the heart control to remove a Favorite. In an offline-download management sheet, the existing Remove downloaded audio action removes the active profile's managed offline files and pending downloads. It does not delete playlists, Favorites or separately exported files.

A Clear listening history action exists in the legacy Settings/history sheet and also clears the active profile's statistics and recommendations. That Settings entry is not exposed by the current normal navigation; this policy does not claim a new deletion control has been added. There is no current per-profile delete-account action or single in-app wipe-everything control.

To remove all private Syntix data, use Android Settings, Apps, Syntix, Storage, Clear storage/Clear data, or uninstall the app. Android wording varies by phone. Remove exported audio/MP4/backup files separately in the destination file manager or cloud provider. External services' records, other apps' copies and already shared files are not removed by clearing Syntix storage. Android controls device access grants and some residual system records.

## Backup and security limits

The manifest sets `allowBackup=false` and defines no `dataExtractionRules` or `fullBackupContent` rules. No developer cloud backup/sync is configured. Android/OEM device-transfer behavior can vary; this is not a guarantee that every device-transfer mechanism is disabled. Private preferences/files and the SQLite database use Android app storage protections, without app-level profile passwords. Completed managed offline audio has the encryption described above; other local records are not separately encrypted by Syntix. Keep the phone itself secured.

## Children

Syntix is intended for people aged 13 and older (13+), and is not intended for children under 13. By creating a local profile, you confirm you are at least 13. If local law or an external service requires a higher age or a parent/guardian's permission, those requirements also apply. The app records your acknowledgement locally; it does not verify your age or provide a verified parental-consent mechanism. If you believe information about a child under 13 requires attention, contact mittal.rishabh2010@gmail.com. A 13+ minimum is not a certification of worldwide children's-privacy compliance or a store content rating.

## Questions and changes

Contact mittal.rishabh2010@gmail.com with privacy questions. Include only information needed to explain your request; do not send account passwords or tokens. Future changes to the app's data handling require updating this policy and its effective date. This draft must be completed and reviewed before public publication.


## Google Play update checks

For installations attributed to Google Play, Syntix uses Google's Play In-App Updates SDK to check for eligible updates when the app returns to the foreground and to display Google's immediate-update flow. Google's documentation lists device metadata, application version, and installed module/asset-pack information as used to determine update availability and size. Google Play handles these requests and installation under its own terms and privacy practices. The app does not send listening history, searches, profiles or playlists to the update SDK. Store/network failure does not block offline playback. Users of other installers do not receive this Play-specific flow.

Song-add recommendations use playlist names, artists and retained listening metadata to construct YouTube Music catalog queries. More results are requested when the recommendation grid reaches the end; dismissing the grid cancels its pending request.
