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

## Testing auto-update locally

1. Install `MarketFlow-Setup-1.0.0.exe` on a test PC. The bot reports `v1.0.0`.
2. Publish `v1.0.1` (tag + `.exe` asset) to this repo — `releases/latest` now returns v1.0.1.
3. Launch the bot (or Settings → Check for Updates): it sees v1.0.1 > v1.0.0 and shows
   "Update available" → **Update Now** downloads and quietly installs 1.0.1.
4. Relaunch: bot is v1.0.1, no more prompt.

> The `.exe` is a **release asset**, never committed to the repo — GitHub's commit
> limit is 100 MB per file, but release assets allow up to 2 GB.
> The repository must stay **public** or the bot's unauthenticated API call returns 404.