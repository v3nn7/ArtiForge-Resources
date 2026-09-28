# ArtiForge-Resources

Public resource repository for the **ArtiForge** Minecraft plugin (Paper, 1.21.11).

Copyright (c) 2026 ArtiForge. All Rights Reserved. See [LICENSE](LICENSE).

## Layout

```text
ArtiForge-Resources/
├── manifest.json        # versioned manifest (the plugin fetches this)
├── pack/                # resource pack content (zipped on release)
│   ├── pack.mcmeta
│   └── assets/
│       └── artiforge/
│           ├── items/         # item model definitions (1.21.4+ format)
│           ├── models/item/   # Blockbench-exported models
│           └── textures/item/ # PNG textures
├── models/              # Blockbench sources (.bbmodel)
├── previews/            # render previews (docs only)
├── schemas/             # JSON schemas for manifest/items
└── .github/workflows/   # release automation
```

## Item model chain (Minecraft 1.21.11, modern components)

ArtiForge item `model.id: artiforge:kroliczy_miecz`
-> item_model component = Key("artiforge", "kroliczy_miecz")
-> assets/artiforge/items/kroliczy_miecz.json (item definition)
-> assets/artiforge/models/item/kroliczy_miecz.json (model JSON)
-> assets/artiforge/textures/item/kroliczy_miecz.png (texture)

No legacy CustomModelData, no overrides of vanilla files.

## Replacing vanilla block models

Use standard resource pack files to replace a vanilla block appearance. Put its
blockstate file under `pack/assets/minecraft/blockstates/<block>.json`, a model
under `pack/assets/<namespace>/models/block/`, and textures under
`pack/assets/<namespace>/textures/block/`. The blockstate filename must match
the vanilla block ID. In the ArtiForge server merge, files from
`resources/custom` take precedence over downloaded resources at identical paths.

For example, to change oak planks, define
`pack/assets/minecraft/blockstates/oak_planks.json` pointing its empty variant
to `artiforge:block/oak_planks_custom`, then create
`pack/assets/artiforge/models/block/oak_planks_custom.json` with parent
`minecraft:block/cube_all` and texture `artiforge:block/oak_planks_custom`.
Add the PNG at `pack/assets/artiforge/textures/block/oak_planks_custom.png`.
Blocks with properties need a blockstate entry for each relevant state. After
installing the files on the server, run `/af resources reload` and have players
reload or accept the resource pack. `/af blocks` lists detected block models
and blockstate files.
## Armor (equipment assets)

Wearable items (see `equipment:` in plugin item YAMLs) resolve to:

```text
equipment.asset-id: artiforge:kroliczy
  -> assets/artiforge/models/armor/kroliczy.json   (layers config)
  -> assets/artiforge/textures/entity/armor/kroliczy_layer_1.png (64x32)
  -> assets/artiforge/textures/entity/armor/kroliczy_layer_2.png (64x32, leggings)
```

## Release flow

1. Add/change content under `pack/` (and Blockbench sources under `models/`).
2. Commit to `main`.
3. Tag the release: `git tag v1.0.1 && git push origin v1.0.1`.
4. GitHub Actions zips `pack/` into `artiforge-resources-<version>.zip`
   (plus an evergreen `artiforge-resources.zip` for `pack.host-url`),
   creates a GitHub Release and **automatically updates `manifest.json`**
   (`version`, `pack.url`, `pack.sha256`) on `main`.
5. The plugin downloads the release ZIP on next check/startup,
   verifies SHA-256 and installs it atomically.
   GitHub downtime falls back to the local cache.

## Current items

| ID | Model | Texture | Armor |
|----|-------|---------|-------|
| `kroliczy_miecz` | ✅ | ✅ | — |
