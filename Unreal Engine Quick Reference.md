# Unreal Engine Quick Reference
 
**Authored by:** Kevin Pledger
 
**Verified (and occasionally updated) by:** Claude
 
**Last updated:** October 28, 2026
 
**Status:** Starter draft, written before first real use. Nothing here is field-tested yet — §13 fills in as it gets earned.
 
Translating from Unity, navigation, Blueprints, import, Git, and delivery.
 
---
 
**Constants:** Unreal Engine **5.8.4** (home and work) · Blueprint-first (C++ later) · **centimeters, Z-up** · Windows
 
> **Version note:** 5.8 is the last planned major UE5 release, so 5.8.x hotfixes are the end of the line until UE6. See §12.
 
---
 
## 1. Unity --> Unreal Translation Table
 
Most confusion in the first week is vocabulary. Same ideas, different names.
 
| Unity | Unreal | Note |
|---|---|---|
| GameObject | **Actor** | Anything placed in a level |
| Component | **Component** | Same idea. *Scene* Components have a transform; *Actor* Components don't |
| Prefab | **Blueprint Class** | A Blueprint is a prefab *with its own script attached* |
| Scene | **Level** (`.umap`) | Also called a Map |
| Hierarchy | **Outliner** | |
| Inspector | **Details** panel | |
| Project window | **Content Browser** | `Ctrl` + `Space` opens it as a pop-up drawer |
| MonoBehaviour (C#) | **Blueprint** graph or **C++** class | Unreal does not use C# |
| `Start()` / `Update()` | **Event BeginPlay** / **Event Tick** | |
| `Debug.Log` | **Print String** node (Blueprint) / `UE_LOG` (C++) | |
| Play Mode | **PIE** (Play In Editor) | |
| Timeline | **Sequencer** (Level Sequence asset) | |
| Animator Controller | **Animation Blueprint** | State machines live inside it |
| Shader Graph | **Material Editor** | Build one master material, then make **Material Instances** of it |
| UI Canvas / UGUI | **UMG** (Widget Blueprints) | |
| New Input System | **Enhanced Input** | Input Actions + Input Mapping Contexts — same idea as Unity's action maps |
| Rigidbody | **Simulate Physics** checkbox on the mesh component | |
| Trigger Collider + `OnTriggerEnter` | Collision set to overlap + **On Component Begin Overlap** | Needs **Generate Overlap Events** ✓ on *both* sides |
| Package Manager | **Edit --> Plugins** | |
| Asset Store | **Fab** | |
| ScriptableObject | **Data Asset** | |
| Cinemachine | **Camera Actor** / **Spring Arm** + Camera component | |
| Baked lighting | **Lumen** (dynamic GI, on by default) | Baking is optional, not the default workflow |
 
---
 
## 2. Units and Axes
 
| | Unity | Blender | Unreal |
|---|---|---|---|
| Unit | meter | meter (default) | **centimeter** |
| Up axis | Y | Z | **Z** |
| Handedness | left | right | left |
 
So `1` in a Unity Transform = `100` in an Unreal Transform. A 2 m door is `200` tall. If something is a hundred times too big or too small, it's units, not your model.
 
---
 
## 3. Viewport Navigation
 
| Key | Does |
|---|---|
| **Right Click (hold) + `W` `A` `S` `D`** | Fly — the main way to move. `Q` / `E` = down / up |
| Right Click (hold) + scroll | Change fly speed while flying |
| `F` | Focus on selected (same as Unity) |
| `Alt` + Left drag | Orbit around the focus point |
| `Alt` + Right drag | Dolly zoom |
| Middle drag | Pan |
| `G` | Game view — hides editor icons and gizmos |
| `F11` | Immersive mode — viewport fills the window |
| `Ctrl` + `0`–`9` / `0`–`9` | Save / jump to a camera bookmark |
| `Alt` + `G` / `H` / `J` / `K` | Perspective / front / top / side views |
 
**Camera speed** has a slider in the viewport's top-right corner. If flying feels glacial or hyperactive, that's where to fix it.
 
---
 
## 4. Editor Shortcuts
 
### Transforming
 
| Key | Does |
|---|---|
| `W` / `E` / `R` | Move / rotate / scale gizmo · `Space` cycles them |
| `Ctrl` + `` ` `` | Toggle world / local coordinates |
| `End` | **Drop selected to the floor** |
| `Alt` + drag a gizmo | Duplicate while moving |
| `Ctrl` + `D` | Duplicate in place |
| Hold `V` + drag | Vertex snapping |
| `H` / `Ctrl` + `H` | Hide selected / unhide all (editor only) |
 
Grid, rotation, and scale snap toggles and increments are the small icons along the viewport's top toolbar.
 
### Saving and finding
 
| Key | Does |
|---|---|
| `Ctrl` + `S` | Save the **current level** |
| `Ctrl` + `Shift` + `S` | **Save all** — every modified asset |
| `Ctrl` + `P` | Quick-open any asset by name |
| `Ctrl` + `B` | Show the selected actor's asset in the Content Browser |
 
> **Unreal saves per asset, not per project.** An asterisk on an asset tab or Content Browser icon means unsaved. `Ctrl` + `S` saves only the level — materials and Blueprints you edited stay unsaved. **Use `Ctrl` + `Shift` + `S` by habit.**
 
---
 
## 5. Play In Editor (PIE) & the Lost-Changes Trap
 
| Key | Does |
|---|---|
| `Alt` + `P` | Play in Editor |
| `Alt` + `S` | Simulate — runs physics and logic without possessing a player |
| `Esc` | Stop |
| `Shift` + `F1` | Get your mouse cursor back during PIE |
| `F8` | Eject from the player to fly the editor camera while the game runs |
| `` ` `` (backtick, during PIE) | Console — try `stat fps`, `stat unit`, `t.MaxFPS 60` |
 
**Same trap as Unity:** changes made while playing are thrown away on Stop.
**Unlike Unity, there's an escape hatch:** select the changed actor and press `K` (**Keep Simulation Changes**) before stopping.
 
---
 
## 6. Blueprints Basics
 
| Key / Action | Does |
|---|---|
| Right Click on the graph | Search for any node |
| Drag off a pin, release | Search filtered to nodes that fit that pin |
| `Alt` + Click a pin | Break its connections |
| `Ctrl` + drag a wire | Move the connection to another pin |
| Double-click a wire | Add a reroute node |
| `Q` | Straighten selected connections |
| `C` | Comment box around selected nodes |
| Hold `B` + Left Click | Drop a **Branch** (if/else) node |
| `F7` | **Compile** — the button turns green ✓ when clean |
| `F9` on a node | Breakpoint |
| `Ctrl` + `F` | Find within this Blueprint |
 
**Reading a graph:** white wires are **execution** (the order things happen); colored wires are **data** (red = bool, green = float, blue = object reference, and so on). A node with no white wire into it isn't running.
 
> **Nothing works? Compile, then save.** An uncompiled Blueprint runs its *previous* version in PIE. It is the Blueprint equivalent of Unity's red Console errors.
 
### Starter pattern: walk-into-a-zone trigger
 
The equivalent of `ProximityTrigger.cs` in the Unity reference:
 
1. Create a **Blueprint Class --> Actor**. Add a **Box Collision** component.
2. Select the Box --> Details --> scroll to **Events** --> click `+` beside **On Component Begin Overlap**.
3. From `Other Actor`, drag out --> **Cast To** your player character class (or use **Actor Has Tag** with tag `Player`).
4. Connect the success pin to **Print String** to prove it fires, then replace it with the real action.
5. Compile (`F7`), save, drag into the level, test with `Alt` + `P`.
---
 
## 7. C++ (When You Get There)
 
- Needs **Visual Studio 2022** with the **Game development with C++** workload installed.
- A Blueprint-only project can add C++ any time: **Tools --> New C++ Class**.
- **Live Coding** (`Ctrl` + `Alt` + `F11`) recompiles while the editor stays open.
- The common professional split: core systems in C++, wired together and tuned in Blueprints. For training content, Blueprint-only is often enough.
---
 
## 8. Importing Assets (From Blender and Elsewhere)
 
Drag files into the Content Browser, or **Import** button. Unreal 5.x imports **FBX**, **glTF**, and **USD**.
 
| Import option | Use |
|---|---|
| **Import Uniform Scale** | Fix a units mismatch at import (e.g. `100` for an asset authored in meters that arrives tiny) |
| **Build Nanite** | Turn on for dense static meshes. Leave off for skeletal meshes |
| **Generate Collision** | Auto collision for simple props |
| **Import Materials / Textures** | Fine for a first pass; real materials get rebuilt as Material Instances |
 
### Custom collision from Blender
 
Name a simple hull mesh after its parent with a prefix, export them together, and Unreal uses it as collision:
 
| Prefix | Shape |
|---|---|
| `UCX_` | Convex hull — `UCX_Cart_00` for a mesh named `Cart` |
| `UBX_` | Box |
| `USP_` | Sphere |
| `UCP_` | Capsule |
 
### Blender character quirks (verify with the first real one)
 
- Unreal may add an **extra root bone** named after the Blender armature object. Naming the armature object exactly `Armature` is the common workaround — the FBX exporter skips adding it as a bone.
- Skeletal meshes are where scale surprises show up. Import one test character end to end — mesh, skeleton, one animation — before committing to a pipeline.
---
 
## 9. Project Structure & Git
 
```text
MyProject/
├─ MyProject.uproject   ← double-click to open; holds the engine version
├─ Config/              ← track
├─ Content/             ← track (all assets: .uasset, .umap)
├─ Source/              ← track (only exists in C++ projects)
├─ Plugins/             ← track if you add project plugins
├─ Binaries/            ← IGNORE — rebuilt
├─ Intermediate/        ← IGNORE — rebuilt
├─ Saved/               ← IGNORE — logs, autosaves, local settings
└─ DerivedDataCache/    ← IGNORE — shader/cache data, regenerated
```
 
Use GitHub's official **UnrealEngine.gitignore** template as a starting point.
 
- **`.uasset` and `.umap` are binary.** Track them all with Git LFS. Binary files cannot merge, so two people editing the same asset is a conflict with no good resolution — coordinate, or use LFS file locking.
- Large levels: **World Partition** with **One File Per Actor** stores each placed actor as its own file, so two people can work in the same level without colliding.
- Epic's own preferred version control is Perforce; Git + LFS is workable for a small team. Same GitHub LFS quota warnings as the Git reference §8 apply — Unreal projects get big fast.
> **The Golden Rule of Unreal Git — same rule, different reason:** never move or rename assets in File Explorer. Unreal references assets **by path** (Unity uses GUIDs in `.meta` files). Always move and rename in the **Content Browser**.
>
> Moving inside Unreal leaves **Redirectors** behind at the old paths. Clean them up before committing: right-click the folder --> **Fix Up Redirectors**.
>
> **Moving assets to another project:** right-click --> **Asset Actions --> Migrate**. It copies the dependencies too. Copy-pasting `.uasset` files by hand usually doesn't.
 
**Path and naming rules:**
 
- Project names **cannot contain spaces** (the New Project dialog enforces it).
- Keep the project path **short** — e.g. `C:\UE\ProjectName`. Unreal's internal paths are deep enough to hit Windows' 260-character limit, which fails builds with unhelpful errors.
---
 
## 10. Performance & Editor Settings
 
| Setting | Where | Why |
|---|---|---|
| **Engine Scalability** | Viewport toolbar --> **Settings** (or the Quickstart) | Lower it on a laptop. Editor-only; doesn't change the shipped game |
| **Realtime** toggle | Viewport menu, or `Ctrl` + `R` | Off = viewport stops redrawing constantly; big CPU/GPU saver while editing |
| **Use Less CPU when in Background** | `Edit --> Editor Preferences --> Performance` | On by default — the viewport freezes when another window has focus. Turn it **off** if you watch PIE while in another app |
 
**First open is slow.** A new project, a new engine version, or a new machine means compiling thousands of shaders (progress bar, bottom right). Start it and walk away — same advice as Unity's first Web build.
 
---
 
## 11. Delivering Training Content
 
> ⚠️ **The one that will matter most: Unreal has no browser build.** HTML5 export was removed from the engine years ago. There is **no equivalent of Unity's WebGL target**, so the Unity reference §10 pattern (Web build --> Storyline Web Object) **does not transfer.**
 
Options, in rough order of fit for training:
 
| Route | What it is | Trade-off |
|---|---|---|
| **Rendered video** | **Movie Render Queue** renders a Sequencer cinematic to video or image sequence | Works everywhere, drops straight into Storyline. Not interactive |
| **Packaged desktop build** | **Platforms --> Windows --> Package Project** | Fully interactive. Learners must download and run an `.exe` — likely an IT/security conversation |
| **Pixel Streaming** | Game runs on a GPU server, streams to a browser | Interactive in a browser, but needs server infrastructure and bandwidth per learner |
 
**Decide the delivery route before building**, the same way the Unity reference warns about platform switches — it determines what's worth making interactive at all.
 
### Sequencer (cinematics)
 
1. Toolbar **Cinematics** (clapperboard) button --> **Add Level Sequence**.
2. Drag actors from the Outliner into the Sequencer track list.
3. Add a **Camera Cut** track and a Cine Camera Actor for shots.
4. Set the sequence frame rate (top of Sequencer) to the delivery rate **before** keying.
---
 
## 12. Version Notes
 
| Version | Notes |
|---|---|
| **5.7** (Nov 2025) | **Substrate** materials are production-ready and **on by default** — older tutorials show the legacy material layout, so expect panel differences. PCG is production-ready. Ships an experimental in-editor **AI Assistant** |
| **5.8** (June 2026) | **Current version — 5.8.4.** Last planned major UE5 release. Adds an **Unreal MCP server plugin** (relevant to the existing Blender/Unity MCP workflows). **MegaLights** is production-ready |
| **UE6** | Early access expected around 2027 |
 
**Keep home and work on the same hotfix.** A project saved in a newer engine version won't open in an older one. Patch releases within 5.8 are generally compatible, but matching versions removes the question.
 
**Opening a project in a newer engine version** prompts you to convert it. Choose **Open a Copy** — conversion is one-way. Never convert mid-project without a Git commit first.
 
**Tutorial version drift:** UE4 tutorials are still everywhere. Navigation and Blueprints mostly carry over; menus, rendering (Lumen, Nanite, Substrate), and input (Enhanced Input replaced the old Action/Axis mappings) do not.
 
---
 
## 13. Things I Learned the Hard Way
 
*(Empty until it isn't.)*
 
- 
### Predicted (move up once confirmed)
 
- Forgetting `Ctrl` + `Shift` + `S` and losing material or Blueprint edits.
- Editing a Blueprint, forgetting `F7`, and testing the old version.
- Something 100× the wrong size — units (§2).
- Moving assets in File Explorer (§9).