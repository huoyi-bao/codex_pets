# Syncing This Codex Pets Project

This repo contains Codex Desktop custom pet packages and preview assets.

## What To Sync

The generated pet package for Aqua Ribbon lives here:

```text
pets/aqua-ribbon/
  pet.json
  spritesheet.webp
```

Preview and QA assets live here:

```text
previews/aqua-ribbon/
  contact-sheet.png
  review.json
  validation.json
  gifs/
  videos/
```

The local Codex install copy lives outside the repo:

```text
%USERPROFILE%\.codex\pets\aqua-ribbon
```

## On Another Windows Device

Clone the repo:

```powershell
git clone https://github.com/<your-user>/codex_pets.git
cd codex_pets
```

Install Aqua Ribbon into Codex Desktop:

```powershell
$dest = Join-Path $env:USERPROFILE ".codex\pets\aqua-ribbon"
New-Item -ItemType Directory -Force -Path (Split-Path $dest) | Out-Null
Remove-Item -LiteralPath $dest -Recurse -Force -ErrorAction SilentlyContinue
Copy-Item -LiteralPath ".\pets\aqua-ribbon" -Destination $dest -Recurse
```

Then restart Codex Desktop, or use Force Reload/Refresh in the pet selector.

## Install All Pets From This Repo

```powershell
$petsRoot = Join-Path $env:USERPROFILE ".codex\pets"
New-Item -ItemType Directory -Force -Path $petsRoot | Out-Null
Get-ChildItem .\pets -Directory | ForEach-Object {
  $target = Join-Path $petsRoot $_.Name
  Remove-Item -LiteralPath $target -Recurse -Force -ErrorAction SilentlyContinue
  Copy-Item -LiteralPath $_.FullName -Destination $target -Recurse
}
```

## Validate The Repo

```powershell
python .\scripts\validate_catalog.py
```

Expected result:

```text
catalog ok: 2 pet(s)
```

## Current Aqua Ribbon Package

```text
id: aqua-ribbon
displayName: Aqua Ribbon
spritesheet: pets/aqua-ribbon/spritesheet.webp
atlas: 1536x1872 WebP, 8 columns x 9 rows
```

The generated package was produced with the `hatch-pet` skill and has local QA files in:

```text
previews/aqua-ribbon/review.json
previews/aqua-ribbon/validation.json
```
