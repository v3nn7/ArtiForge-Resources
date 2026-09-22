# Contributing to ArtiForge-Resources

1. Export models from Blockbench in Minecraft: Java Edition format.
2. Place files in the right folders:
   - `pack/assets/artiforge/items/<id>.json`
   - `pack/assets/artiforge/models/item/<id>.json`
   - `pack/assets/artiforge/textures/item/<id>.png` (keep model `texture_size` in sync)
   - Blockbench sources (`.bbmodel`) go to `models/`, renders to `previews/`.
3. Keep `pack.mcmeta` `pack_format` compatible with the Minecraft version
   listed in `manifest.json`.
4. Open a pull request against `main`. Do **not** edit `manifest.json`
   `pack.url`/`pack.sha256` by hand — the release workflow updates them.
5. After merge, a maintainer tags a release (`vX.Y.Z`) to publish.
