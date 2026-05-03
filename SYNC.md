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
catalog ok: 1 pet(s)
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

## How Aqua Ribbon Was Created

The pet was generated with Codex's `hatch-pet` skill. The workflow was:

1. Install and reload the `hatch-pet` skill.
2. Use the character reference images and the approved chibi standing base sprite as identity references.
3. Generate a canonical base sprite.
4. Generate the 9 Codex pet animation rows:
   `idle`, `running-right`, `running-left`, `waving`, `jumping`, `failed`, `waiting`, `running`, and `review`.
5. Generate `running-left` separately instead of mirroring `running-right`, because the character has a one-sided yellow hair ribbon.
6. Finalize with the `hatch-pet` scripts to extract frames, compose the 8x9 atlas, validate it, render previews, and package the pet.

Original creation request:

```text
$hatch-pet create a Codex desktop pet based on these character reference images.

Use the chibi standing base sprite as the main identity reference. The pet should be a small pixel-art-adjacent chibi desktop mascot, not polished anime key art.

Character traits:
short pale aqua-silver hair, bright yellow eyes, yellow-and-black side hair ribbon, loose white rolled-sleeve shirt, dark gray plaid pleated skirt, black thigh-high socks, brown loafers, yellow bracelet, cheerful energetic personality.

Important constraints:
keep her grounded, not floating; no checkerboard background; no shadows; no text; no UI props; keep the outfit and face consistent across all animation rows.
```

The local run folder used during creation was:

```text
%USERPROFILE%\.codex\hatch-pet-runs\aqua-ribbon
```

Key QA outputs from that run were copied into this repo:

```text
previews/aqua-ribbon/contact-sheet.png
previews/aqua-ribbon/review.json
previews/aqua-ribbon/validation.json
previews/aqua-ribbon/gifs/
previews/aqua-ribbon/videos/
```

The final generated Codex package was copied from:

```text
%USERPROFILE%\.codex\pets\aqua-ribbon
```
