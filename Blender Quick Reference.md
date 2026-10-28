# Blender Quick Reference
 
**Authored by:** Kevin Pledger
 
**Verified (and occasionally updated) by:** Claude
 
**Last updated:** October 28, 2026
 
Navigation, the G/R/S grammar, modeling, export to Unity and Unreal, and getting un-lost.
 
---
 
**Constants:** Blender **5.x** via the **Microsoft Store** (auto-updates — don't trust a pinned version number) · **default keymap, left-click select** · numpad keys listed, laptop alternatives in §1
 
> ⚠️ **This file is general Blender knowledge. For anything headed into RHWM, `docs/PIPELINE.md` (Blender export conventions) wins.** §9 here is the short, general form.
 
---
 
## 1. Viewport Navigation
 
| Key | Does |
|---|---|
| Middle Click (hold) + drag | Orbit |
| `Shift` + Middle drag | Pan |
| Scroll / `Ctrl` + Middle drag | Zoom |
| `Numpad .` | **Frame selected** — the Blender equivalent of Unity's `F` |
| `Home` | Frame everything |
| `Numpad 1` / `3` / `7` | Front / Right / Top view (`Ctrl` + same = opposite side) |
| `Numpad 5` | Toggle perspective / orthographic |
| `Numpad 0` | Look through the active camera |
| `Ctrl` + `Alt` + `Numpad 0` | Snap the active camera to the current view |
| `Numpad /` | Local view — isolate selection (press again to return) |
| `` ` `` (backtick) | **View pie menu** — all the numpad views, no numpad needed |
| `Shift` + `` ` `` | Fly/walk navigation (WASD; `Esc` cancels back to where you started) |
 
**No numpad? No middle mouse?** `Edit --> Preferences --> Input`: **Emulate Numpad** (top-row numbers become view keys — but then they stop switching vertex/edge/face, see §5) and **Emulate 3 Button Mouse** (`Alt` + Left Click = Middle Click).
 
**Framing a camera shot:** `N` sidebar --> **View** tab --> **Lock Camera to View**. Now navigating moves the camera itself. **Turn it off when done**, or the next orbit wrecks your shot.
 
---
 
## 2. Selecting
 
| Key | Does |
|---|---|
| Left Click | Select |
| `Shift` + Click | Add to selection / make active (click twice to deselect) |
| `A` | Select all |
| `Alt` + `A` | Deselect all |
| `Ctrl` + `I` | Invert selection |
| `B` | Box select |
| `C` | Circle (paint) select — scroll to resize, Right Click or `Esc` to exit |
| `Alt` + Click (Edit Mode) | Select edge loop |
| `Ctrl` + `Alt` + Click (Edit Mode) | Select edge ring |
| `L` (Edit Mode) | Select linked geometry under the cursor |
| `Ctrl` + `L` (Edit Mode) | Select everything linked to the current selection |
 
**Active vs. selected:** the *active* object is the brighter orange outline — the last one clicked. Many operations (parenting, joining, copying modifiers) act on "selected onto active," so **click the target last**.
 
---
 
## 3. Moving, Rotating, Scaling — the Grammar
 
Blender transforms are sentences: **verb --> axis --> amount --> confirm.**
 
| Step | Keys | Example |
|---|---|---|
| Verb | `G` (grab/move) · `R` (rotate) · `S` (scale) | `R` |
| Axis | `X` / `Y` / `Z` — press **twice** for local axis · `Shift` + axis = everything *except* that axis | `Z` |
| Amount | Type a number (negatives allowed) | `90` |
| Confirm / cancel | Left Click or `Enter` / Right Click or `Esc` | `Enter` |
 
So `R` `Z` `9` `0` `Enter` rotates 90° around Z. `G` `G` (Edit Mode) is **edge/vertex slide**.
 
| Key | Does |
|---|---|
| Hold `Ctrl` while transforming | Snap |
| Hold `Shift` while transforming | Precision (slow) |
| `Shift` + `Tab` | Toggle snapping on/off |
| `O` | Toggle proportional editing (scroll during transform to resize the falloff) |
| `Alt` + `G` / `R` / `S` | Clear location / rotation / scale |
| `Ctrl` + `A` | **Apply** menu — bake transforms into the mesh (see the warning below) |
| `.` (period) | Pivot point pie (median, individual origins, 3D cursor…) |
| `Shift` + `S` | Snap pie — cursor to selected, selection to cursor, cursor to world origin |
| `F9` | Reopen the last operation's settings panel |
| `Shift` + `R` | Repeat last action |
 
> ⚠️ **Apply your scale.** An object scaled in Object Mode has Scale ≠ 1, and modifiers (Bevel, Solidify, Array) and exports all inherit that distortion. Before modifiers or export: `Ctrl` + `A` --> **Scale** (or **All Transforms**). This is the single most common source of "why is my bevel lopsided" and "why is it the wrong size in Unity."
 
---
 
## 4. Modes, Adding, Deleting, Organizing
 
| Key | Does |
|---|---|
| `Tab` | Toggle Object Mode ↔ Edit Mode |
| `Ctrl` + `Tab` | Mode pie (Sculpt, Weight Paint, Pose…) |
| `Shift` + `A` | Add menu (mesh, light, camera, empty…) — lands at the **3D cursor** |
| `X` or `Delete` | Delete |
| `Shift` + `D` | Duplicate (then move; Right Click drops it in place) |
| `Alt` + `D` | **Linked** duplicate — shares mesh data; edit one, all change |
| `Ctrl` + `J` | Join selected into the active object |
| `P` (Edit Mode) | Separate — split selection into its own object |
| `M` (Object Mode) | Move to collection |
| `H` / `Alt` + `H` / `Shift` + `H` | Hide / unhide all / hide everything unselected |
| `F2` | Rename active object |
| `F3` | **Search every operator by name** — when you know what you want but not where it lives |
| `Ctrl` + `Space` | Maximize the area under the mouse (again to restore) |
| `N` / `T` | Toggle sidebar / toolbar |
| `Ctrl` + `Z` / `Ctrl` + `Shift` + `Z` | Undo / redo (`Edit --> Undo History` to jump back several steps) |
 
**Origin:** Object Mode, Right Click --> **Set Origin** (to geometry, to 3D cursor…). Moving geometry in Edit Mode does **not** move the origin — which is why rotated objects sometimes swing around a point off in space.
 
**Splitting a mesh for separate materials in Unity** (the shared-`Element`-slot problem in the Unity reference §6): Edit Mode --> select the part --> `P` --> **Selection**.
 
---
 
## 5. Edit Mode Modeling
 
| Key | Does |
|---|---|
| `1` / `2` / `3` (top row) | Vertex / edge / face select mode |
| `E` | Extrude |
| `I` | Inset faces |
| `Ctrl` + `R` | Loop cut (scroll for more cuts, click, then slide) |
| `K` | Knife (`Enter` to confirm) |
| `Ctrl` + `B` | Bevel edges (`Ctrl` + `Shift` + `B` = bevel vertices) — scroll for segments |
| `F` | Fill — make a face/edge from selection |
| `M` | Merge menu — **By Distance** removes duplicate vertices |
| `Shift` + `N` | Recalculate normals outward (`Ctrl` + `Shift` + `N` = inward) |
| `Alt` + `E` | Extrude menu (along normals, individual faces…) |
| `Ctrl` + `V` / `Ctrl` + `E` / `Ctrl` + `F` | Vertex / edge / face menus |
| `Alt` + `Z` | X-ray toggle — select through the mesh |
 
> **Inside-out faces?** Viewport **Overlays** dropdown --> **Face Orientation**. Blue = facing out (good), red = facing in. Red faces often render invisible or black in Unity and Unreal because backfaces are culled. Fix: select all, `Shift` + `N`.
 
---
 
## 6. Modifiers (Non-Destructive Edits)
 
Properties panel --> wrench tab --> **Add Modifier**. The stack runs **top to bottom**, so order changes the result.
 
| Modifier | Typical use |
|---|---|
| **Mirror** | Model half, get both halves — enable **Clipping** so center vertices don't drift apart |
| **Subdivision Surface** | Smooth a low-poly cage. Shortcut: `Ctrl` + `1`–`5` in Object Mode sets the level |
| **Bevel** | Catch-light edges without hand-modeling them (needs applied scale — §3) |
| **Solidify** | Give a plane thickness |
| **Array** | Repeat along an axis (shelves, railings, stairs) |
| **Boolean** | Cut or combine shapes. Messy topology; good for hard-surface blockouts |
| **Decimate** | Reduce poly count — the fix for scan-quality meshes that blow up a Web build |
| **Weld** | Merge-by-distance, non-destructively |
 
**Apply** a modifier: hover over it --> `Ctrl` + `A`. The FBX exporter has an **Apply Modifiers** checkbox, so for export you usually don't need to apply them by hand.
 
---
 
## 7. Shading, Materials, Rendering
 
| Key / Path | Does |
|---|---|
| `Z` | Shading pie: Wireframe · Solid · Material Preview · Rendered |
| `Shift` + `Z` | Toggle wireframe |
| `F12` | Render a still image |
| `Ctrl` + `F12` | Render the animation |
| Properties --> **Render** tab | Choose **EEVEE** (fast, real-time-ish) or **Cycles** (path-traced, slow, accurate) |
 
**What survives export to a game engine:** a **Principled BSDF** with image textures plugged into Base Color, Roughness, Metallic, and Normal (through a Normal Map node). Procedural node trees — noise, gradients, math nodes — **do not export.** To keep them, bake them to image textures first (Cycles --> Render tab --> **Bake**).
 
**Textures going missing on another machine:** `File --> External Data --> Pack Resources` embeds them in the `.blend`. Or keep relative paths and move the texture folder with the file.
 
---
 
## 8. Animation Basics
 
| Key | Does |
|---|---|
| `I` | Insert keyframe on the default channels (location, rotation, scale) — no menu since Blender 4.1 |
| `K` | Keying set menu (choose exactly what gets keyed) |
| `Alt` + `I` | Delete keyframe on the current frame |
| `Space` | Play / pause |
| `Shift` + `Left Arrow` | Jump to start |
| `Left` / `Right Arrow` | Step one frame |
| `Up` / `Down Arrow` | Jump to next / previous keyframe |
| `T` (Graph Editor / Dope Sheet) | Interpolation (constant, linear, Bézier) |
 
> **Auto Keying** is the record button in the Timeline — same trap as Unity's record button. **Turn it off when done**, or every layout nudge becomes a keyframe.
 
**Frame rate** lives in Properties --> **Output** tab. Match it to the engine target (RHWM is **60 fps**) *before* animating; retiming afterward stretches every key.
 
---
 
## 9. Exporting to a Game Engine
 
`File --> Export --> FBX (.fbx)`. Save these settings as an **Operator Preset** (the `+` beside the presets dropdown at the top of the export dialog) so you only set them once.
 
### Before every export
 
- [ ] `Ctrl` + `A` --> **All Transforms** on static props (§3)
- [ ] Normals checked with Face Orientation (§5)
- [ ] Origin where the engine should pivot (usually base-center for props)
- [ ] Objects named meaningfully — the names become the engine's names
### Settings worth knowing
 
| Setting | Recommended | Why |
|---|---|---|
| **Limit to → Selected Objects** | ✓ | Export only what you meant to |
| **Object Types** | Mesh, Armature (Empty if needed) | ⚠️ **Leave Camera and Light unchecked** — this prevents the bundled-lights problem in the Unity reference §6 at the source |
| **Apply Scalings** | FBX Units Scale | Lands at scale `1` in-engine |
| **Apply Modifiers** | ✓ | Bakes the modifier stack into the exported mesh |
| **Path Mode / Embed Textures** | Copy + Embed | Textures travel inside the FBX (Unity extracts them to `.fbm`) |
| **Bake Animation** | ✓ only if the object is animated | Otherwise it's dead weight |
 
### Unity: the −90° rotation
 
Blender is **Z-up**; Unity is **Y-up**. Exported with defaults, props often arrive with **Rotation X = −90** on the root. Pick one fix:
 
1. Unity side: FBX importer --> Model tab --> **Bake Axis Conversion** ✓
2. Blender side: FBX export --> **Apply Transform** ✓ (marked experimental — fine for static meshes, can misbehave with armatures)
### Unreal: different units, same up-axis
 
Unreal is **Z-up like Blender** but works in **centimeters**. Static meshes exported with the settings above generally arrive at correct size and orientation. Character rigs have known quirks (an extra root bone, scale surprises) — see `Unreal Quick Reference.md` §8 and verify with your first character before trusting a pipeline.
 
---
 
## 10. Python & Scripting
 
Relevant for writing scripts and for reading what Blender MCP is doing.
 
| Where | What |
|---|---|
| **Scripting** workspace (top tabs) | Text editor + Python console + Info log |
| **Info** editor | Logs the Python equivalent of **every click you make** — the fastest way to learn the API |
| `Edit --> Preferences --> Interface --> Python Tooltips` | Hover any button to see its Python path |
| Hover a field + `Ctrl` + `Shift` + `C` | Copy its full data path |
 
**Blender 5.0 API changes that break older scripts and add-ons:**
 
- The EEVEE engine identifier is `BLENDER_EEVEE` again. It was `BLENDER_EEVEE_NEXT` in 4.2–4.5, so scripts written in that window check for the wrong name.
- Dictionary-style access to add-on property storage was removed — `bpy.context.scene['cycles']` no longer reaches Cycles' settings. Use the attribute form (`scene.cycles`).
If an add-on or MCP connection breaks right after an auto-update, suspect the add-on's compatibility with the new version before suspecting your file.
 
---
 
## 11. "I'm Lost" — Rescue Table
 
| Symptom | Fix |
|---|---|
| Can't find the object | Select it in the Outliner, hover viewport, `Numpad .` |
| View is sideways / upside down | `` ` `` pie --> pick a view, or `Numpad 1` |
| Everything else vanished | You're in local view — `Numpad /` |
| Object won't move where expected | Check you're in the right mode (`Tab`) and the pivot (`.`) |
| Keys do the wrong thing | Mouse is over a different editor — shortcuts follow the **mouse**, not the last click |
| Whole UI is one giant panel | `Ctrl` + `Space` to un-maximize |
| Crashed before saving | `File --> Recover --> Auto Save` (interval in `Preferences --> Save & Load`) |
| Saved over something important | The previous save is beside it as `filename.blend1` — rename to `.blend` |
 
---
 
## 12. Things I Learned the Hard Way
 
- The Microsoft Store version **auto-updates**, and an update can break add-ons (Blender MCP included) without touching your files. After an update, first launch may offer to import the previous version's settings — accept it, or your preferences and add-ons look "gone."
- Shortcuts act on the editor **under the mouse**. Half of "Blender ignored my keypress" is the cursor sitting over the Outliner.
- Scale applied, normals checked, cameras and lights left out — before every export.
- 