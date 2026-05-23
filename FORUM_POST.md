# [Support] Khord — Self-Hosted Music Sharing for Unraid

## What is Khord?

Khord is a self-hosted music sharing app. Share a song once and your followers can listen on whichever streaming service they use — Spotify, Apple Music, YouTube Music, Deezer, and more. Sign in with an email address and password — no third-party accounts required. All data lives in a single SQLite database on your server.

Features include cross-platform song sharing, mixtapes (collaborative playlists), Apple Music playlist import, upvoting, an admin panel for managing users and access control, and multiple UI themes.

---

## Installation

Khord is a single container. Install it from Community Applications and set the **Data Path** (default: `/mnt/user/appdata/khord/data`).

---

## Requirements

- A **reverse proxy** with a valid TLS certificate (NGINX Proxy Manager, Swag, Traefik, etc.) pointed at port 3000.
- `PUBLIC_APP_URL` set to your public HTTPS URL, e.g. `https://khord.yourdomain.com`.
- `OWNER_EMAILS` set to your email address — the first account you register with that email gets admin access.

---

## Key Settings

| Setting | Notes |
|---|---|
| **App URL** | Required. Your public HTTPS URL. |
| **Owner Emails** | Comma-separated email addresses that get admin access to `/admin`. |
| **Data Path** | Where the SQLite database and thumbnail cache are stored. |
| **Database File Name** | `khord.db` by default. Only change if you need to rename the database file. |
| **Spotify Client ID / Secret** | Optional. From developer.spotify.com. Enables Spotify URL resolution when sharing songs. |
| **YouTube API Key** | Optional. YouTube Data API v3 key from console.cloud.google.com. Enables YouTube Music links. Also enable YouTube Music in the admin panel Settings tab. Free quota is ~100 searches/day. |
| **Apple Music Developer Token** | Optional. MusicKit JWT from developer.apple.com → Keys. Enables Apple Music playlist import. Requires an Apple Developer account ($99/yr). Tokens are valid up to 6 months. After setting, enable in the admin panel Settings tab. |
| **Theme** | Requires a container restart to apply. Options: `dark` (default), `slate`, `navy`, `teal`, `emerald`, `rose`, `violet`, and several light variants. |

---

## Access Control

By default, anyone can register with an email address. You can restrict this from the admin panel:

- **Max Users** — cap the number of registered users (0 = unlimited)
- **Invite Only** — new users must be approved before they can sign in
- **Bans** — block individual users by username or email from the admin panel (takes effect immediately, no restart needed)

---

## Troubleshooting

**Container won't start**
Check that `PUBLIC_APP_URL` is set — it's the only required variable.

**Album art not loading**
Some third-party CDN URLs can be unreliable. You can disable album art entirely from the admin panel (Admin → Settings → Disable Album Art) without a restart.

**Can't access the admin panel**
Make sure `OWNER_EMAILS` includes the email address you registered with. If you registered before setting `OWNER_EMAILS`, you can set `role = 'admin'` directly in the database or re-register with a matching email on a fresh install.

---

## Links

- GitHub: https://github.com/khordapp/khord
- Issues / bug reports: https://github.com/khordapp/khord/issues
