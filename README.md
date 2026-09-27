# MarketFlow Releases

Release artifacts for the MarketFlow bot installer.

## Repository Structure

- `MarketFlow-Setup-1.0.0.exe` — Initial release installer
- `release-manifest.json` — Version manifest

## Creating a New Release

1. Build new `.exe` and place in this repo
2. Create a GitHub Release with the version tag (e.g., `v1.0.1`)
3. Upload the `.exe` as a release asset
4. Call `POST /admin/downloads` on the server with the release info

## GitHub Releases API

The bot checks `https://api.github.com/repos/abubakkarsaddique766-dev/MarketFlow-releases/releases/latest` for updates.

Admin creates releases via `POST /admin/downloads` on the server, which can automatically create GitHub Releases if `GITHUB_TOKEN` is configured.
