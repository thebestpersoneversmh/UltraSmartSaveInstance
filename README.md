# UltraSmartSaveInstance

A modified build of **UniversalSynSaveInstance (USSI)** that correctly saves **UnionOperations** (CSG `MeshData2` geometry) and **Terrain**.

## Usage

```lua
local synsaveinstance = loadstring(game:HttpGet("https://raw.githubusercontent.com/thebestpersoneversmh/UltraSmartSaveInstance/refs/heads/main/saveinstance.lua", true), "saveinstance")()
local Options = {} -- Full option list @ https://luau.github.io/UniversalSynSaveInstance/api/SynSaveInstance
synsaveinstance(Options)
```

## What's different from the normal save instance

- **Unions render correctly.** Re-enabled `gethiddenproperty` during the save (it was being disabled unconditionally) so the union's `MeshData2` is actually read, and stopped `IgnoreSharedStrings` from dropping the `MeshData2` / `ChildData2` SharedStrings. On executors that can't read union mesh data, unions fall back to a visible bounding-box Part instead of being invisible.
- **Terrain** `SmoothGrid` / `PhysicsGrid` are serialized.
- **Faster, lighter saves** — the file is assembled with a table buffer instead of repeated string concatenation, fixing the `O(n²)` growth that caused "not enough memory" on large games.

>[!NOTE]
> `ChildData` is `NotReplicated`, so client-side saves render unions but can't make them editable/separable in Studio.

## Credits
- [luau/UniversalSynSaveInstance](https://github.com/luau/UniversalSynSaveInstance)
- [RealSlimShady2000/SaveInstanceMODIFIEDFullUnionSupport](https://github.com/RealSlimShady2000/SaveInstanceMODIFIEDFullUnionSupport/)
- [Claude](https://github.com/claude)
