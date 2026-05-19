# khord-unraid

[Unraid Community Applications](https://unraid.net/community/apps) XML templates for [Khord](https://github.com/khordapp/khord).

Two templates are included:

| Template | Description |
|---|---|
| [`khord.xml`](khord.xml) | Main Khord app — SvelteKit web server on port 3000 |
| [`khord-indexer.xml`](khord-indexer.xml) | Firehose indexer — writes AT Protocol records to SQLite |

Both containers share the same data directory (SQLite database). Install both for the full experience. Khord works without the indexer, but the feed will be slower (direct PDS fetches instead of the AppView).

---

## Installing via Community Applications

Search for **Khord** in the Community Applications plugin. Both templates will appear.

If the templates aren't listed yet, add the repository URL manually:

1. Open Community Applications → Settings → Enable additional repositories
2. Add: `https://raw.githubusercontent.com/khordapp/khord-unraid/main`

## Manual install

Download the XML files and import them in Unraid's Docker tab → Add Container → Template URL.

Or apply them directly from the raw URLs:

- `https://raw.githubusercontent.com/khordapp/khord-unraid/main/khord.xml`
- `https://raw.githubusercontent.com/khordapp/khord-unraid/main/khord-indexer.xml`

## Setup

1. Install **khord-indexer** first — set the Data Path to `/mnt/user/appdata/khord/data`
2. Install **khord** — set the same Data Path so both containers share the SQLite database
3. Point your Unraid reverse proxy (NGINX Proxy Manager, Swag, Traefik, etc.) at **khord** on port 3000
4. Set `PUBLIC_APP_URL` to your public HTTPS URL — AT Protocol OAuth requires it

See the [Khord admin guide](https://github.com/khordapp/khord/blob/main/docs/admin.md) for the full reference — environment variables, streaming integrations (Spotify, YouTube Music, Apple Music), themes, access control, admin panel walkthrough, and backup.

## Notes

- These containers have no built-in reverse proxy — Khord requires HTTPS for AT Protocol OAuth, so an existing reverse proxy on Unraid is expected
- The Data Path must match between the two containers exactly — they read and write the same `khord.db` file
- Both images are multi-arch (`linux/amd64`, `linux/arm64`) — works on standard x86 Unraid servers and ARM
