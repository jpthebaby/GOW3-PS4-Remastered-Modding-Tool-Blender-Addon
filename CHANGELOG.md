# Changelog

## v2.6.6 – October 2026
- Texture Edit lists **only the textures found in your edited folder**, grouped by kind, plus the ones that can't be edited (cube maps / other formats). No more scrolling through every texture.

## v2.6.5 – October 2026
- **Texture Edit for everything**: 62 groups / 195 files – all Kratos outfits (incl. Fear / Soul), gods, bosses, enemies (with their Soul versions), weapons and items. Weapons and items have **All files (every upgrade level)**.
- **One folder instead of one picker per texture**: edit the extracted PNGs, keep their names, pick the folder. Files are matched by the `TX…` code in their name; only matched textures are packed, exactly as painted (alpha included).
- Costume-menu rename also for texture mods of Kratos's outfits.

## v2.6.4 – October 2026
- **Mesh Edit / Texture Edit** switch in *1. Game Directory*. Texture Edit hides Merge Mesh and always packs the game's original mesh.
- **Mod info** in *6. Pack WAD & Mod*: Author (saved with Save INI), Description and Version. The mod's `README.txt` now starts with Mod Name / Game / Author / Description / Version.

## v2.6.3 – October 2026
- New name: **JP - GOW 3 PS4 Remastered Modding Tool - Blender Add-on** (sidebar tab still *JP GOW3 Modding*).
- **Add Dummy Cube (Pelvis)** for low-poly characters without separate legs.
- Region meshes show their game-vertex count in a tooltip next to Head / Body / Legs / Arms.
- **Pieces one by one**: with Hide Armors off, keep or remove Belt Piece, Boots, Shin Plate, Boot Wings, Bracers, Fleece, Skirt and Hermes Boots separately; the same for Eyes, Beard and Mouth.

## v2.6.2 – October 2026
- Tangents follow the UVs like the game's own models, including mirrored UV islands – fixes dark patches with real normal maps.

## v2.6.1 – October 2026
- Normal maps already in the game's orange layout (like the extracted *Normal* PNGs) are packed as they are instead of being converted twice.

## v2.6 – October 2026
- **Weapon glow**: *Glow* picker (black = no glow, colour = glows in that colour; empty = no glow).
- **Blades of Athena**: *Extra Layer* picker (empty = the Diffuse).

## v2.5 – October 2026
- **Weapons**: *Characters / Weapons* switch. Blades of Exile (all 5 upgrade levels at once), Blades of Athena and Blade of Olympus – import the game blade, model yours in its place, check, merge, texture and pack.

## v2.4 – October 2026
- **Kratos-style culling** (on by default): every body part gets a tight culling sphere around its new geometry, so arms and legs no longer vanish in cutscene close-ups.
- Safer **Fit to Limit**: only the areas that don't fit, never below 70% in one run, stops when it can't improve.
- Triangles whose bone mix fits no slot no longer block Merge – they go to the nearest slot.

## v2.3 – October 2026
- **Real game joints**: `Kratos_GameSkeleton` sits on Kratos's real joints read from the game (before: hips 13 cm, knees / elbows / wrists 4–5 cm off – the cause of torn knees and elbows).
- **Update Skeleton** for scenes made with older versions.
- **Check Joints / Fix Joint Weights** and **Test Bend**.
- Merge maps weights onto the joints Kratos's skin uses: pelvis below the waist, twist joints in the upper arms.

## v2.2 – October 2026
- **Change outfit name**: your name instead of "Kratos" in the costume selection (all 16 languages).

## v1.7.2 – October 2026
First public release.
- New **About / Credits** panel (version, YouTube / Patreon / Discord links).
- Mod folders now include a `README.txt` saying what the mod replaces, when it was built and with which add-on version.
- Complete user guide on the repository page.
- Supports **Kratos – Default Mesh** only.

## v1.7 – October 2026
- **Fit to Limit**: reduces only the areas weighted to bones that ran out of room, on a `_fit` copy.
- Live game-vertex counts (UV seams included).
- 52-bone `Kratos_GameSkeleton`.
- Bone-aware packing of the body parts.

## v1.5 – October 2026
- *By Body Region* placement (Head / Body / Legs & Hips / Arms & Hands meshes).
- **Check / Fix Finger Order**; hand bones moved to the game's real pivots.

## v1.4 – October 2026
- Texture Edit: one texture set for all meshes, dummy normal / specular / occlusion maps.

## v1.0 – October 2026
- First version: extract, import, merge, textures, pack WAD and mod folder.
