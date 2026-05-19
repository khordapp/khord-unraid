# [Support] Khord — Decentralized Music Sharing for Unraid

## What is Khord?

Khord is a self-hosted music sharing platform built on the AT Protocol (the same network as Bluesky). You share a song once and your followers can listen on whichever streaming service they use — Spotify, Apple Music, YouTube Music, Deezer, and more. There's no central database; records live in each user's AT Protocol identity, so your instance is just the interface and local feed cache.

Features include cross-platform song sharing, setlists (collaborative playlists), Apple Music playlist import, upvoting, an admin panel for managing users and access control, and multiple UI themes.

---

## Installation

Khord is two containers that share a SQLite database:

- **khord** — the web app (install this first)
- **khord-indexer** — the firehose subscriber that powers the fast feed

Both are available in Community Applications. Set both containers' **Data Path** to the same directory (default: `/mnt/user/appdata/khord/data`) so they share the database.

---

## Requirements

- A **reverse proxy** with a valid TLS certificate (NGINX Proxy Manager, Swag, Traefik, etc.) pointed at port 3000. AT Protocol OAuth requires a publicly accessible HTTPS URL — the app will not work over plain HTTP.
- A **Bluesky/AT Protocol account** (free at bsky.app) to sign in.
- `PUBLIC_APP_URL` set to your public HTTPS URL, e.g. `https://khord.yourdomain.com`.

---

## Key Settings

| Setting | Notes |
|---|---|
| **App URL** | Required. Your public HTTPS URL. Must match the AT Protocol OAuth redirect URI exactly. |
| **Owner DIDs** | Your AT Protocol DID — grants access to the `/admin` panel. Find it at: `https://bsky.social/xrpc/com.atproto.identity.resolveHandle?handle=your.handle` |
| **Data Path** | Must be identical in both khord and khord-indexer containers. |
| **Database File Name** | `khord.db` by default. Only change if you need to rename the database file — must match in both containers. |
| **Spotify Client ID / Secret** | Optional. From developer.spotify.com. Enables Spotify URL resolution when sharing songs. |
| **YouTube API Key** | Optional. YouTube Data API v3 key from console.cloud.google.com. Enables YouTube Music links. Also enable YouTube Music in the admin panel Settings tab. Free quota is ~100 searches/day. |
| **Apple Music Developer Token** | Optional. MusicKit JWT from developer.apple.com → Keys. Enables Apple Music playlist import. Requires an Apple Developer account ($99/yr). Tokens are valid up to 6 months. After setting, enable in the admin panel Settings tab. |
| **Theme** | Requires a container restart to apply. Options: `dark` (default), `slate`, `navy`, `teal`, `emerald`, `rose`, `violet`, and several light variants. |

---

## Access Control

By default, anyone with an AT Protocol account can register. You can restrict this from the admin panel or via container variables:

- **Max Users** — cap the number of registered users (0 = unlimited)
- **Invite Only** — new users must be approved before they can sign in
- **Allowed DIDs** — explicit allowlist
- **Banned DIDs** — blocklist (live bans can also be managed from the admin panel without a restart)

---

## Troubleshooting

**OAuth redirect fails / "invalid redirect URI"**
Make sure `PUBLIC_APP_URL` exactly matches the URL you're accessing the app from, including the protocol (`https://`) and no trailing slash.

**Feed shows "unavailable" or falls back to slow loading**
The khord-indexer container is not running, or its Data Path doesn't match khord's. Check both containers are running and sharing the same `/data` directory.

**Album art not loading**
Some third-party CDN URLs can be unreliable. You can disable album art entirely from the admin panel (Admin → Settings → Disable Album Art) without a restart.

**Container won't start**
Check that `PUBLIC_APP_URL` is set — it's the only required variable.

---

## Links

- GitHub: https://github.com/khordapp/khord
- Issues / bug reports: https://github.com/khordapp/khord/issues
