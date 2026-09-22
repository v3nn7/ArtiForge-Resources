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

| ID | Model | Texture |
|----|-------|---------|
| `kroliczy_miecz` | ✅ | ✅ |
| `inferno_blade` | ✅ | ❌ (missing — add `textures/item/inferno_blade.png`) |
