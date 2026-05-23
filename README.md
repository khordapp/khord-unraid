# khord-unraid

[Unraid Community Applications](https://unraid.net/community/apps) XML template for [Khord](https://github.com/khordapp/khord).

| Template | Description |
|---|---|
| [`khord.xml`](khord.xml) | Khord app — SvelteKit web server on port 3000 |

---

## Installing via Community Applications

Search for **Khord** in the Community Applications plugin.

If the template isn't listed yet, add the repository URL manually:

1. Open Community Applications → Settings → Enable additional repositories
2. Add: `https://raw.githubusercontent.com/khordapp/khord-unraid/main`

## Manual install

Download the XML file and import it in Unraid's Docker tab → Add Container → Template URL.

Or apply it directly from the raw URL:

- `https://raw.githubusercontent.com/khordapp/khord-unraid/main/khord.xml`

## Setup

1. Install **khord** — set the Data Path to `/mnt/user/appdata/khord/data`
2. Point your Unraid reverse proxy (NGINX Proxy Manager, Swag, Traefik, etc.) at **khord** on port 3000
3. Set `PUBLIC_APP_URL` to your public HTTPS URL
4. Set `OWNER_EMAILS` to your email address — the first account registered with that email gets admin access

See the [Khord admin guide](https://github.com/khordapp/khord/blob/main/docs/admin.md) for the full reference — environment variables, streaming integrations (Spotify, YouTube Music, Apple Music), themes, access control, admin panel walkthrough, and backup.

## Notes

- This container has no built-in reverse proxy — an existing Unraid reverse proxy is expected
- The image is multi-arch (`linux/amd64`, `linux/arm64`) — works on standard x86 Unraid servers and ARM
