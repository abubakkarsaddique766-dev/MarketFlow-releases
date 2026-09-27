# MarketFlow Releases

Public repository that hosts the MarketFlow bot installer. This repo exists so the
bot can check for updates through the public GitHub Releases API — **no GitHub token
is needed in the client or on the server**.

## How updates work

1. **Publish a release** on github.com (this repo):
   - Tag: `v1.0.1` (version must be incremented over the bot's `app/version.py`)
   - Upload the built installer `MarketFlow-Setup-1.0.1.exe` as a **release asset**
   - Changelog goes in the release description/body
2. **Record it in the admin panel** (`Admin → Bot Downloads → Add New Version`):
   - Version: `1.0.1` · Filename: `MarketFlow-Setup-1.0.1.exe`
   - Download URL: the asset URL
     `https://github.com/abubakkarsaddique766-dev/MarketFlow-releases/releases/download/v1.0.1/MarketFlow-Setup-1.0.1.exe`
   - is_latest: Yes
3. **The bot** checks `https://api.github.com/repos/abubakkarsaddique766-dev/MarketFlow-releases/releases/latest`,
   compares the tag with its running version, and prompts the user to download+install when newer.
4. **The website dashboard** fetches `GET /api/website/download` (the Supabase record) and shows the
   Download button with the same GitHub URL.

## Important notes

- The `.exe` is uploaded as a **release asset**, never committed to the repo —
  GitHub's commit limit is 100 MB per file, but release assets allow up to 2 GB.
- The repository must stay **public** or the bot's unauthenticated API call returns 404.
- `release-manifest.json` is metadata only (a human-readable history).