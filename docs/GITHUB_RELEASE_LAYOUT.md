# GitHub Release Layout (FinLibrary)

Use this exact structure for every tag/release.

## Release tag

- Tag format: `v<pluginVersion>`
- Example: `v0.1.0.0`

## GitHub Release assets

Upload exactly one install artifact for Jellyfin:

- `FinLibrary_<version>.zip`
- Example: `FinLibrary_0.1.0.0.zip`

Optional debug artifact:

- `FinLibrary_<version>_symbols.zip`

## Zip content layout

The main zip should contain plugin files at zip root:

- `FinLibrary.dll`
- `FinLibrary.pdb` (optional)
- any additional runtime dependency `.dll` files (if your plugin adds any)

## Local build + packaging (PowerShell)

```powershell
dotnet publish .\FinLibrary.sln -c Release

$version = "0.1.0.0"
$publishDir = ".\FinLibrary\bin\Release\net9.0\publish"
$zipName = "FinLibrary_$version.zip"

Compress-Archive -Path "$publishDir\*" -DestinationPath ".\$zipName" -Force
Get-FileHash ".\$zipName" -Algorithm SHA256
```

Copy the SHA256 value into `manifest.json` under `versions[0].checksum`.

## manifest.json update per release

For each new version:

1. Add a new object at the top of `versions`.
2. Set `version` to your plugin version.
3. Set `targetAbi` to your Jellyfin server ABI line.
4. Set `sourceUrl` to the release asset URL.
5. Set `checksum` to the SHA256 of that zip.

Example URL pattern:

`https://github.com/Sleepmode/FinLibrary-Plugin/releases/download/v<version>/FinLibrary_<version>.zip`

## Publish steps

1. Commit updated `manifest.json`.
2. Push commit to `master` (or your release branch).
3. Create tag `v<version>`.
4. Create GitHub Release from that tag.
5. Upload `FinLibrary_<version>.zip`.
6. If you host plugin manifest in this repo (GitHub Pages/raw), Jellyfin can fetch updates from it.
