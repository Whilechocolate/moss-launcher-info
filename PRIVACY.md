# Privacy and credential handling

Last updated: 30 October 2026. This describes the current Moss Launcher 0.3.2 private preview implementation.

## Microsoft and Minecraft accounts

Sign-in opens Microsoft's authorization page in the user's system browser. The launcher does not provide a password-entry form and does not collect Microsoft account passwords.

MSAL's credential cache is encrypted with Electron `safeStorage` using Windows system encryption. A small remembered player-profile record is also encrypted locally. The active Minecraft session credential is held in the main process and passed to the local game process for authenticated launch. Access and refresh tokens are not sent to the renderer UI or to a MOSS-operated account server.

Signing out removes the launcher's local OAuth cache and remembered player-profile files. It does not sign the user out of Microsoft websites in the browser or delete their game installations. Operating-system access to the user's session and running game processes remains relevant to credential security.

## Local files

Settings, instance records, themes, world bookmarks, and launcher-managed game files are stored locally. Existing Minecraft directories are accessed only through the user's association/import actions. Resource management and repair can modify associated instance directories; supported repairs keep backups inside the instance.

Modpack imports read the archive and may download resources declared by its manifest. Local terrain viewing reads existing world region files; the terrain renderer does not upload those region files to a MOSS server.

A configured CurseForge API key is encrypted locally and used for CurseForge API requests. It is not a Microsoft login credential and is not included in this public repository.

## External services

Depending on the action and configuration, the launcher communicates with Microsoft identity services, Xbox Live, Minecraft Services, official Minecraft download endpoints, an optional BMCLAPI download mirror, Modrinth, CurseForge, and mod-loader metadata or installer providers. These providers receive the network requests needed for the selected operation and handle them under their own policies. Authentication credentials are sent to the relevant Microsoft/Xbox/Minecraft services, not to resource mirrors.

Authentication requests use Electron's Chromium networking and respect Windows system proxy settings. HTTPS certificate validation remains enabled. A configured proxy may process connection information according to its own configuration and policies.

The optional friend tunnel exchanges pairing data manually and uses WebRTC. Pairing data can contain network addresses. A configured STUN provider may receive connectivity requests; the peer can receive the network information required to establish the connection. Only share pairing data with the intended friend. There is no public lobby or hosted TURN service provided by this launcher.

## Diagnostics and contact

The authorization network check sends anonymous requests to fixed service endpoints without account tokens. Displayed diagnostics contain the service stage, hostname, HTTP status or connection code, and elapsed time. They do not intentionally include authorization codes, passwords, or access/refresh tokens.

The launcher does not implement an analytics or advertising service. This GitHub information repository is hosted by GitHub, which processes visits and interactions under its own policies.

For project questions, contact the repository maintainer through GitHub Issues. For application review, use the email provided privately in the review form. Never post credentials or credential cache files publicly.
