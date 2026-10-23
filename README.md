# JP - GOW 3 PS4 Remastered Modding Tool - Blender Add-on

**A free Blender add-on that puts your own character into *God of War III Remastered* as Kratos (PC, gow3_pc port).**
Extract Kratos, rig your character to the real game skeleton, check and fit the vertex limits, pack your textures, and write a ready-to-play mod folder – all from one sidebar in Blender.

> **Current version: Kratos only.** v1.7.2 replaces **Kratos – Default Mesh** (`R_HERO00.WAD`). Other outfits, weapons and characters are not supported yet.

> This is an early version I made for my own use. I'd love to share it with you so you can test it.
> — **Gamer JP**

[![YouTube](https://img.shields.io/badge/YouTube-@jpthehero-red?logo=youtube)](https://www.youtube.com/@jpthehero)
[![Patreon](https://img.shields.io/badge/Patreon-gamerjp-orange?logo=patreon)](https://www.patreon.com/c/gamerjp)
[![Discord](https://img.shields.io/badge/Discord-join-5865F2?logo=discord)](https://discord.gg/uBTutBA8VX)

![JP - GOW 3 PS4 Remastered Modding Tool - Blender Add-on v1.7.2 – sidebar panels](docs/panels.png)

---

## Contents

1. [Features](#features)
2. [Requirements](#requirements)
3. [Download](#download)
4. [Installation](#installation)
5. [Workflow at a glance](#workflow-at-a-glance)
6. [Panel 1 – Game Directory](#panel-1--game-directory)
7. [Panel 2 – WAD Process](#panel-2--wad-process)
8. [Panel 3 – Import Model](#panel-3--import-model)
9. [Preparing your character (rigging rules)](#preparing-your-character-rigging-rules)
10. [Panel 4 – Merge Mesh](#panel-4--merge-mesh)
11. [Vertex limits and Fit to Limit](#vertex-limits-and-fit-to-limit)
12. [Panel 5 – Texture Edit](#panel-5--texture-edit)
13. [Panel 6 – Pack WAD & Mod](#panel-6--pack-wad--mod)
14. [Testing in game, updating and removing a mod](#testing-in-game-updating-and-removing-a-mod)
15. [Files and folders](#files-and-folders)
16. [Messages and troubleshooting](#messages-and-troubleshooting)
17. [Known limits of v1.7.2](#known-limits-of-v172)
18. [Quick checklist](#quick-checklist)
19. [Credits](#credits) · [Disclaimer](#disclaimer) · [License](#license)

---

## Features

- **Game Directory** – set the port exe and game folder once; they're saved in an INI and loaded automatically.
- **Mod loader check** – shows whether your port version loads God of War III mods (current port versions do out of the box).
- **Extract** Kratos's model (`R_HERO00.WAD`) and **all his textures as PNG**.
- **Import** the **real game skeleton** (`Kratos_GameSkeleton`, 52 bones) plus Kratos's body, armour and face parts with their game weights.
- **Merge your own character** into Kratos's mesh:
  - **By Bone Weights** (one collection) or **By Body Region** (Head / Body / Legs & Hips / Arms & Hands meshes),
  - **Check Vertex Limit** – counts vertices like the game does (UV seams included) and paints what doesn't fit **red**,
  - **Fit to Limit** – reduces only the areas that don't fit, on a copy (your original stays untouched),
  - **Check / Fix Finger Order** – repairs rigs with mixed-up finger groups,
  - keep or hide Kratos's **armour** and **eyes / beard / mouth** (kept pieces can be edited too).
- **Texture Edit** – one texture set for the whole character, or a different image per game texture. Dummy normal / specular / occlusion maps built in, blood overlays switched off automatically, DXT encoding with mipmaps.
- **Pack WAD** – checks the WAD the way the game reads it before writing it.
- **Pack Mod Files** – writes a ready mod folder (`<Mod Name> vN`) straight into the port's `mods` folder, never overwriting older builds.
- Runs entirely inside Blender – **no extra tools or installs**.

## Requirements

| Item | Details |
|---|---|
| Blender | **4.2 or newer** (the add-on uses Blender's built-in Python and numpy) |
| Game files | Your own extracted PS4 game folder, **CUSA01715** (tested on v1.02). It must contain `eboot.bin` and the `EXEC\WAD\PS4_LE` folder. |
| gow3_pc port | The PC port exe (`God of War III.exe`). Its folder holds the `mods` folder and the add-on's work folder `JPGow3 Temp`. |
| Your character | A mesh with a UV map and textures (colour map at least). It will be rigged to the game skeleton – see [rigging rules](#preparing-your-character-rigging-rules). |
| Disk space | About 2× the size of `R_HERO00.WAD` plus its PNG textures, next to the port exe. |
| OS | Windows 10 / 11 |

You need **your own copy of the game**. This add-on contains **no game files**.

## Download

Go to the [**Releases**](../../releases) page and download:

| File | What it is |
|---|---|
| **`JP_GoW3_Modding_Master_v1.7.2.zip`** | The Blender add-on – install it as a zip, **do not unzip it** |

## Installation

1. If an older version is installed: **Edit → Preferences → Add-ons**, remove the old **JP GOW3 Modding** / **JP - GOW 3 PS4 Remastered Modding Tool - Blender Add-on**, then restart Blender.
2. **Edit → Preferences → Add-ons →** drop-down arrow (top right) **→ Install from Disk…** → pick the zip.
3. Tick **JP - GOW 3 PS4 Remastered Modding Tool - Blender Add-on** to enable it.
4. Restart Blender.
5. In the 3D View press **N** → tab **JP GOW3 Modding** (the sidebar tab keeps the short name).

The zip also holds `JP_GoW3_Modding.ini.example`. You don't need to edit it by hand – the **Save INI** button writes the settings file for you.

**Sidebar panels, from top to bottom:**

| Panel | Used for |
|---|---|
| 1. Game Directory | Where the port exe and the game files are; mod loader status |
| 2. WAD Process | Choose character and outfit, extract the WAD and its textures |
| 3. Import Model | Bring the game skeleton and Kratos's meshes into Blender |
| 4. Merge Mesh | Check the vertex limits, fit your character, merge it into the WAD |
| 5. Texture Edit | Pick your images for each game texture and pack them |
| 6. Pack WAD & Mod | Verify the WAD and write the mod folder |
| About / Credits | Version, author and links |

## Workflow at a glance

**1 Game Directory → 2 WAD Process → 3 Import Model → rig your character → 4 Merge Mesh → 5 Texture Edit → 6 Pack WAD & Mod**

1. **Once:** set the PC port exe and game directory, **Save INI**. The panel should show **Mod loader patched**.
2. **Extract WAD + Textures** – copies `R_HERO00.WAD` into `JPGow3 Temp` and exports Kratos's textures as PNG.
3. **Import Model** – adds `Kratos_GameSkeleton` and Kratos's meshes.
4. Rig your character to `Kratos_GameSkeleton` in its **own collection**.
5. In panel 4 pick your collection, then **Check Vertex Limit**. If it doesn't fit, **Fit All to Limit**. Run **Check / Fix Finger Order**, then **Merge Mesh**.
6. In panel 5 pick your textures and **Pack Textures**.
7. **Pack WAD**, type a **Mod Name**, **Pack Mod Files**.
8. Start the game through the port and test. (You launch the game yourself; the add-on never does.)

> **Note:** the buttons are only active when the step before them is done: Import needs Extract, Pack WAD needs Merge, Pack Mod Files needs Pack WAD. A greyed-out button means a previous step is missing.

> **Tip:** after changing anything in your character, run **Merge Mesh** again, then **Pack WAD** and **Pack Mod Files**. Merge keeps textures you already packed, so you only pack textures again if the images changed.

## Panel 1 – Game Directory

| Option | What it does |
|---|---|
| **INI** | The settings file. Empty = `JP_GoW3_Modding.ini` next to the add-on. It is read automatically about a second after Blender starts. |
| **Load INI** / **Save INI** | Read both paths from the file / write them. Save once and you never have to type the paths again. |
| **PC Port EXE** | `God of War III.exe` of the gow3_pc port. |
| **Game Directory** | The extracted PS4 game folder (the one with `eboot.bin` and `EXEC`). |
| Status lines | *PC port exe found* and *Game files found (eboot.bin + EXEC\WAD)* must both show a green tick before you can extract. *Mods folder:* shows where your mods will be written. |
| **Fix Mod Loader** | Appears only on old port versions (see below). |

### Mod loader

Current versions of the gow3_pc port load God of War III mods out of the box (the port's developer added support for it), so the panel shows **Mod loader patched** and there is nothing to do.

Only on an **old port version** does the panel show *Mod loader unpatched - mods won't load* together with a **Fix Mod Loader** button. The best fix is to **update the port**. Clicking **Fix Mod Loader** also works on those old versions: it adds the small change to `scripts\mods.py` and keeps a backup as `mods.py.original_backup`.

> **Important:** if the loader can't load God of War III mods, your mod folder is written but the game ignores it. **Pack Mod Files** warns you about this as well.

## Panel 2 – WAD Process

| Option | What it does |
|---|---|
| **Character** / **Outfit** | In v1.7.2 this is **Kratos – Default Mesh** only. |
| `R_HERO00.WAD (MG_b826bd6e_0)` | The game file and the mesh entry inside it that will be replaced. |
| **Extract WAD + Textures** | Copies the WAD into `JPGow3 Temp` (twice: an untouched `original` and a `work` copy) and saves every texture as PNG. It also fills the texture list in panel 5. |
| **Open Extracted Folder (JPGow3 Temp)** | Opens the work folder in Explorer – handy to look at Kratos's textures as a template for your own. |

> **Important:** extracting again **resets** the work WAD to the original and clears the merged / packed state. Your Blender scene and your texture choices stay. Only extract again when you want a clean start.

## Panel 3 – Import Model

**Import Model** reads the extracted WAD and builds this scene:

| Collection / object | Contents |
|---|---|
| `GoW3_Skeleton` › `Kratos_GameSkeleton` | The game armature. Bones are named like `j004 spine 3`, `j067 arm right elbow`, `j136 leg right knee`: the number is the game joint, the words say where it is. |
| `GoW3_Kratos_DefaultMesh_Body` | Kratos's skin parts (Body_Head, Body_Hand_R, …). These are the **slots** your character is poured into. |
| `GoW3_Kratos_DefaultMesh_Armor` | Skirt, boots, bracers, fleece, belt piece. |
| `GoW3_Kratos_DefaultMesh_FaceExtras` | Eyes, beard, teeth, tongue, eyelid piece. |

Each imported part is skinned to the skeleton and carries its limits as custom properties (*Object Properties › Custom Properties*): `vertex_limit` and `triangle_limit`. Textures are linked so you see Kratos as in game.

After importing, the panel reminds you of the one rule that matters: *rig your character to Kratos_GameSkeleton, in another collection, using only the bones whose names start with `j`.*

> **Important:** don't move, rotate, scale or edit the bones of `Kratos_GameSkeleton`. The check compares it with the game: if bones were moved you get *"Kratos_GameSkeleton was edited (N bones moved) - re-import it"*. Delete it and click **Import Model** again.

## Preparing your character (rigging rules)

The game moves your character with Kratos's skeleton and Kratos's animations, so your mesh must be **weighted to the game bones**. Follow these rules and the merge will work first time:

| Rule | Why |
|---|---|
| Put your character's meshes in **their own collection** (e.g. `Custom`), not inside the GoW3_ collections. | Panel 4 takes that collection as input. |
| Parent / Armature-modifier the meshes to `Kratos_GameSkeleton`. | So you can test poses in Blender exactly like the game. |
| Vertex groups must have the **exact bone names**, e.g. `j135 leg right thigh`. Use only bones starting with `j`. | Bones starting with `x` are helpers the game doesn't skin to. Groups with other names are ignored. |
| Match Kratos's proportions and pose: scale/align your character to the imported Kratos body. | Joints bend where Kratos's joints are. Elbows, knees and wrists must sit on the bones. |
| Apply transforms (*Ctrl+A › All Transforms*) on your meshes. | Positions are read in world space. |
| Every mesh needs a **UV map**. | Meshes without UVs can't be fitted or merged. |
| Remove **shape keys** before Fit to Limit. | Decimate can't be applied to meshes with shape keys. |
| Max 4 bone influences per vertex; weights below 0.1 are dropped. | The game stores 4 weights per vertex. |
| Fingers: index, middle, ring, little must be in the right order (see **Check / Fix Finger Order**). | Swapped finger groups make fingers bend across each other. |

### Useful bones

| Body area | Bone names (vertex group names) |
|---|---|
| Hips / pelvis | `j001 pelvis`, `j002 root hips` |
| Spine / neck / head | `j003 spine 1`, `j004 spine 3`, `j005 head neck lower`, `j006 head neck upper`, `j008 head jaw` |
| Right arm | `j065` / `j066 arm right shoulder 1/2`, `j096` / `j098 arm right twist 1/2`, `j067 arm right elbow`, `j068 arm right wrist` |
| Left arm | `j102` / `j103 arm left shoulder 1/2`, `j130` / `j131 arm left twist 1/2`, `j104 arm left elbow`, `j105 arm left wrist` |
| Fingers | thumb = finger 1, index = 2, middle = 3, ring = 4, little = 5; joints a, b, c – e.g. `j069 arm right finger 2a` |
| Right leg | `j135 leg right thigh`, `j136 leg right knee`, `j137 leg right ankle`, `j138 leg right toe` |
| Left leg | `j149 leg left thigh`, `j150 leg left knee`, `j151 leg left ankle`, `j152 leg left toe` |
| Eyes | `j046 head eyeball left`, `j057 head eyeball right` |
| Skirt (cloth) | `j166 … j217 skirt …` – for skirts, coats and loincloths that should swing like Kratos's skirt |

> **Tip:** test before merging. Select `Kratos_GameSkeleton`, Pose Mode, rotate the upper arm, elbow, thigh, knee and head. If something stretches or stays behind, fix the weights first – the game will look exactly the same.

## Panel 4 – Merge Mesh

| Option | What it does |
|---|---|
| **Placement** | **By Bone Weights** (one collection, recommended) or **By Body Region** (one mesh per region). |
| **Custom** | The collection with your rigged character. |
| **Hide Armors** | On: Kratos's skirt, boots, bracers, fleece and belt piece are removed. Off: they stay. |
| **Hide Eyes, Beard, Mouth** | On: Kratos's eyes, beard, teeth, tongue and eyelid piece are removed. Off: they stay. |
| **Slots** | Optional per-mesh slot: Auto (by weights) or force a mesh into one Kratos slot. |
| **Check Vertex Limit** | Does it fit? Paints what doesn't fit **red**. The result of the last check is shown below it (green tick = fits). |
| **Fit All to Limit** | Reduces a copy of your character until it fits (see [Vertex limits](#vertex-limits-and-fit-to-limit)). |
| **Check / Fix Finger Order** | Fixes swapped finger vertex groups. |
| **Merge Mesh** | Writes your character into the work WAD. |

### Placement modes

| Mode | How it works | Use when |
|---|---|---|
| **By Bone Weights** | Pick one collection. Every triangle goes into the Kratos slot whose bones it is weighted to (hands into the hand slots, head into the head slot …). The safe default. | Almost always. |
| **By Body Region** | Pick one mesh for each region: **Head**, **Body**, **Legs & Hips**, **Arms & Hands**. Triangles are still placed by their bones, but the report and the per-region **Fit … to Limit** buttons work region by region, and each region shows its game vertex count. | You split your character into region meshes and want to reduce one area only (e.g. just the head). |

### Hide Armors / Hide Eyes, Beard, Mouth

Both are **on** by default: your character replaces Kratos completely. Turn one off to keep those Kratos pieces in the game. Kept pieces can even be edited: move or sculpt the imported armour / face pieces in Blender and the edit is written into the game – as long as the **vertex count stays the same**. If the count changed, that piece keeps its original shape and Merge tells you *"N armour piece(s) kept original, see console"*.

### Slots (optional)

With **By Bone Weights**, every mesh in your collection gets a slot dropdown. **Auto** (default) places each triangle by its weights. Choosing a slot puts that whole mesh into that one Kratos part and shows its limit ("max N verts / N tris"). The mesh must then only use bones that slot allows (hover the dropdown to see them). Leave it on Auto unless you have a reason.

### Merge Mesh

**Merge Mesh** runs the same check first and stops if anything doesn't fit. When it fits, it writes the new mesh into the work WAD, keeps already packed textures, and reports e.g. *"Merged 13,850 triangles into 21 body parts, armour hidden, eyes/beard/mouth hidden"*. A report is saved as `merge_report.json` in `JPGow3 Temp`.

## Vertex limits and Fit to Limit

The game can't grow Kratos's mesh: each body slot has a fixed number of vertices and triangles. Your character is poured into these slots by its bone weights, so it doesn't matter how many meshes you have – what counts is how many vertices are weighted to **each group of bones**.

**Game vertices** are more than Blender's vertex count: every UV seam and hard edge splits a vertex in two. The panel shows both ("N game vertices (M in Blender + UV seams)").

| Slot | Max vertices | Max triangles | Main bones |
|---|---:|---:|---|
| Foot R | 730 | 1,056 | leg right knee, ankle, toe |
| Foot L | 729 | 1,056 | leg left knee, ankle, toe |
| Forearm R | 858 | 1,276 | arm right elbow, wrist, fingers … |
| ShoulderPiece | 236 | 384 | arm right elbow, right twist 2, arm left elbow, left twist 2 |
| Forearm L | 862 | 1,276 | arm left elbow, wrist, fingers … |
| Head | 1,495 | 1,968 | spine 3, head neck lower, head neck upper, head jaw … |
| Pelvis Thighs | 1,267 | 1,786 | pelvis, root hips, thighs, knees |
| Toes R | 57 | 66 | leg right ankle, toe |
| Toes L | 57 | 66 | leg left ankle, toe |
| Chest Back UpperArms | 1,647 | 2,563 | root hips, spine 1, spine 3, neck, shoulders, twist … |
| ShoulderPiece L | 207 | 336 | arm left shoulder 1/2, elbow, twist 1/2 |
| Hand R | 864 | 1,174 | arm right wrist, fingers |
| Hand L | 847 | 1,174 | arm left wrist, fingers |
| Face detail ×8 | 1,736 | 2,137 | head neck upper, jaw, eyeballs |
| **Total** | **11,592** | **16,318** | |

Region totals (By Body Region mode):

| Region | Max vertices | Max triangles |
|---|---:|---:|
| Head | 3,231 | 4,105 |
| Body | 2,090 | 3,283 |
| Legs & Hips | 2,840 | 4,030 |
| Arms & Hands | 3,431 | 4,900 |

### Reading the check

| Message | Meaning / what to do |
|---|---|
| *Fits: N triangles* | All good – click **Merge Mesh**. |
| *Vertex limit is more: X of N triangles don't fit (mostly bone A, bone B …). Click Fit to Limit* | Too many vertices are weighted to those bones. The red faces in the viewport are the ones that don't fit. Use **Fit All to Limit** or reduce that area yourself. |
| *Slot S is over its limit … this slot can't use: bones* | A mesh forced into a slot is too big, or uses bones that slot can't hold. Set it back to Auto or reduce it. |
| *… WARNING: right hand finger groups are out of order* | Click **Check / Fix Finger Order**. |

### Fit to Limit

**Fit All to Limit** (or **Fit Head to Limit** etc. in region mode) makes a **copy** of your character and decimates only the areas weighted to bones that ran out of room, checking again after every step, until everything fits. Your original meshes are **hidden, not changed**, and the copy becomes the new input, so you can always go back.

- Remove shape keys first – otherwise: *"'mesh' has shape keys - remove them first"*.
- If it already fits you get *"Already fits … nothing to reduce"*.
- Fit reduces triangles; thin details (straps, blades, fingers) can get holes if they had to lose a lot. For the best result reduce heavy areas yourself first (Decimate, remove hidden inner faces, merge UV islands to cut seams) and let Fit do the last bit.
- Fewer UV seams = fewer game vertices. Marking fewer seams is often the cheapest way to fit.

### Check / Fix Finger Order

Looks at where each finger's vertex group really sits on the hand. If index, middle, ring and little are swapped (common with rips and auto-rigs), it renames the groups so they match – weights are kept. Merge again afterwards. When all is well: *"Finger order is correct (index, middle, ring, little)"*.

## Panel 5 – Texture Edit

The panel lists Kratos's textures after you extract. There are two ways to use it.

### Same textures for all meshes (default)

| Option | What it does |
|---|---|
| **Same textures for all meshes** | One image of each kind is used for every Kratos texture of that kind. Best when your character uses one texture set (or one atlas). |
| **Diffuse** | Your colour map. Always needed in this mode. |
| **Dummy Normal / Dummy Specular / Dummy Occlusion** | Ticked (default) = a neutral map is generated (flat normal, low shine, no occlusion). Untick to pick your own image. |
| **Pack Textures** | Encodes everything into the work WAD. |

### Per-texture mode

Untick **Same textures for all meshes** to see every game texture grouped by kind (Diffuse, Normal, Specular, Occlusion, Blood) with its size, e.g. *Body (1024x1024)*. Pick an image for each one you want to replace. Each kind has a **Use Dummy … for all** switch. Empty slots keep Kratos's texture – the panel tells you how many (*"N empty slot(s) keep Kratos's texture"*).

### Good to know

- Images are resized to the game texture's size automatically and encoded as DXT with all mipmaps. Use square, power-of-two images (1024, 2048) for the sharpest result.
- Your UVs must match your images: if your character uses several texture sets, either use per-texture mode or combine them into one atlas first.
- **Blood overlays are switched off automatically** – they follow Kratos's body layout and would show as blotches on your character.
- Normal maps: standard OpenGL style (green up). If yours are DirectX style (green down), tick **Flip Normal Green (DirectX)** (shown when Dummy Normal is off).
- Hide Eyes, Beard, Mouth off: the kept eyes/teeth use the Head/Body textures.
- Hide Armors off: shared images fill only the Body / Head textures; the armour keeps Kratos's textures.
- You can pack textures before or after merging – the two don't overwrite each other.

> **Important:** don't leave Kratos's own normal or specular maps on a new character: his muscles and scars will show through as lines and blotches. Keep the dummies on unless you have maps made for your character's UVs.

## Panel 6 – Pack WAD & Mod

| Option | What it does |
|---|---|
| **Pack WAD** | Reads the work WAD back the way the game does and compares it with the original. If anything is wrong it stops with *"Check failed: …"*; otherwise it writes the final WAD to `JPGow3 Temp\output` and shows e.g. *"13,850 triangles drawn, layout identical"*. |
| **Mod Name** | The mod folder name. |
| **Add version (vN)** | Adds the next free number (`MyMod v2`, `v3` …) so older builds are never overwritten. The line below shows the exact folder name. |
| **Pack Mod Files** | Writes the mod folder in the port's `mods` folder. |
| **Open Mods Folder** | Opens the mods folder in Explorer. |

The mod folder layout:

```
mods\MyMod v3\dvdroot_ps4\EXEC\WAD\PS4_LE\R_HERO00.WAD
mods\MyMod v3\README.txt      (what it replaces, build date, credits)
```

## Testing in game, updating and removing a mod

1. Make sure panel 1 shows **Mod loader patched** (it does on current port versions).
2. In the port's mod list, enable your new mod and **untick other mods that replace `R_HERO00.WAD`** – only one can win.
3. Start the game through the port and load a save. Check: walking, combat, climbing, a cutscene, and the pause menu.

**What to look at**

- Elbows, knees, shoulders and hips bending smoothly (bad weights show as spikes or stretching).
- Hands and fingers gripping the blades correctly (finger order).
- Missing faces: usually normals flipped in Blender or faces that didn't fit and were dropped – run Check again.
- Odd lines or blotches: Kratos's normal/specular maps still in use – use the dummies.

**Updating a mod:** change your character in Blender → **Merge Mesh** → (**Pack Textures** if images changed) → **Pack WAD** → **Pack Mod Files**. With **Add version (vN)** on, a new folder (v2, v3 …) is made – enable the new one and untick the old one in the port.

**Removing a mod:** untick it in the port's mod list, or delete its folder from `mods`. The original game files are never changed by the add-on – all work happens in copies.

## Files and folders

| Path (next to the port exe) | Contents |
|---|---|
| `JPGow3 Temp\Kratos_DefaultMesh\original\R_HERO00.WAD` | Untouched copy of the game file |
| `…\work\R_HERO00.WAD` | The WAD being edited (merge and textures go here) |
| `…\textures\` | Kratos's textures as PNG (from Extract) |
| `…\dummy_textures\` | The generated dummy normal / specular / occlusion maps |
| `…\output\R_HERO00.WAD` | The checked, final WAD (from Pack WAD) |
| `…\merge_report.json` | What Merge did (slots, triangles, hidden pieces) |
| `…\state.json` | Which steps are done (extracted / merged / textures / packed) |
| `mods\<Mod Name vN>\` | The finished mod (from Pack Mod Files) |
| `JP_GoW3_Modding.ini` (add-on folder) | Your saved paths |
| `scripts\mods.py.original_backup` | Backup made by Fix Mod Loader (old port versions only) |

## Messages and troubleshooting

| Message / problem | Fix |
|---|---|
| *Check failed: WAD layout changed* / *… out-of-range indices* | The work WAD is damaged: Extract again, then Merge and Pack Textures again. |
| *PC port exe not set / not found*, *Game directory not set / not valid* | Check the paths in panel 1. The game directory is the folder containing `eboot.bin`. |
| *INI not found* / *INI has no [GoW3] section* | Set the paths by hand and click **Save INI**. |
| *Not found: …R_HERO00.WAD* | The game folder is incomplete or points one level too high/low; it must contain `EXEC\WAD\PS4_LE`. |
| *Extract first* | Run **Extract WAD + Textures** (panel 2). |
| *Kratos_GameSkeleton was edited (N bones moved) - re-import it* | Delete the skeleton, **Import Model** again, and re-point your Armature modifiers to the new one. |
| *Vertex limit is more: …* | **Fit All to Limit** or reduce the named area. |
| *Pick the Custom collection first* | Choose your collection in panel 4 (**Custom**). |
| *No mesh with a UV map to fit* | Add a UV map to your meshes. |
| *'…' has shape keys - remove them first* | *Object Data Properties › Shape Keys* › remove all (or apply them). |
| *Pick the Diffuse texture* | Same textures mode needs a Diffuse image. |
| *Packed N textures, M failed (console)* | *Window › Toggle System Console* shows which image failed – usually a missing file or unsupported format. Use PNG/JPG/TGA. |
| *Merge the mesh first* / *Pack the WAD first* | Do the steps in order: Merge → Pack WAD → Pack Mod Files. |
| *WARNING: the mod loader is not patched* | Update the gow3_pc port (or panel 1 → **Fix Mod Loader** on an old version). |
| *mods.py changed in a port update - patch it by hand* | Update the gow3_pc port to the latest version, which loads God of War III mods by itself. Ask on Discord if it persists. |
| Mod doesn't show in game | Mod enabled in the port? Other mods replacing `R_HERO00.WAD` unticked? Panel 1 shows **Mod loader patched**? |
| Character looks inside-out or has holes | Recalculate normals (*Mesh › Normals › Recalculate Outside*); re-check that everything fits. |
| Lines / blotches on the skin | Dummy Normal / Dummy Specular on. |
| Fingers bend across each other | **Check / Fix Finger Order**, then Merge again. |
| The tab doesn't appear | Restart Blender after installing; press **N** in the 3D View; check the add-on is enabled. |

The add-on prints details to Blender's system console (*Window › Toggle System Console*), lines start with `[JP GoW3]`. Include that text when you ask for help on [Discord](https://discord.gg/uBTutBA8VX).

## Known limits of v1.7.2

- **Only Kratos – Default Mesh** (`R_HERO00.WAD`) can be replaced. Other outfits, weapons and characters are not supported yet.
- The total vertex budget is Kratos's (see [Vertex limits](#vertex-limits-and-fit-to-limit)). Very detailed characters must be reduced.
- Your character uses Kratos's bones and animations – long hair, capes or tails only move if weighted to existing bones (e.g. the skirt bones).
- In some cutscenes parts of the character can be hidden when the camera is very close, because the game uses Kratos's own visibility bounds.
- Glow maps are not edited by this version.

## Quick checklist

- [ ] Paths set, both green ticks, INI saved, mod loader patched
- [ ] Extract WAD + Textures
- [ ] Import Model
- [ ] Character in its own collection, transforms applied, UV map, no shape keys
- [ ] Weighted to `j` bones of `Kratos_GameSkeleton` only; pose test in Blender OK
- [ ] Panel 4: collection picked, Hide Armors / Hide Eyes, Beard, Mouth as wanted
- [ ] Check Vertex Limit → Fit All to Limit if needed → Check / Fix Finger Order
- [ ] Merge Mesh
- [ ] Panel 5: Diffuse picked, dummies on (or own maps), Pack Textures
- [ ] Pack WAD (check passed)
- [ ] Mod Name, Pack Mod Files
- [ ] Enable the mod in the port, untick other `R_HERO00` mods, test in game

## Credits

- **Gamer JP** – author ([YouTube](https://www.youtube.com/@jpthehero) · [Patreon](https://www.patreon.com/c/gamerjp) · [Discord](https://discord.gg/uBTutBA8VX))
- **gow3_pc** port and its authors – for making God of War III playable and moddable on PC
- Santa Monica Studio / Sony Interactive Entertainment – *God of War III*

Please credit **Gamer JP** when you share mods made with this add-on.

## Disclaimer

This is a fan-made tool, not affiliated with or endorsed by Sony Interactive Entertainment or Santa Monica Studio.
*God of War* is a trademark of Sony Interactive Entertainment LLC. The add-on contains no game data; use extracted assets for personal modding only.

## License

See [LICENSE.txt](LICENSE.txt). Free to use; you may share mods made with it (credit **Gamer JP**), but please don't re-upload, modify or sell the add-on itself.
