# Hachidori in SubMiner

The `subminer` branch maintains SubMiner integration changes on top of the
upstream revision recorded in `SOURCE.json`. SubMiner pins this repository as
its `vendor/hachidori` submodule. `UPSTREAM-README.md` is the original project
introduction. HoshiDicts remains an unmodified upstream submodule.

`bun run build:hachidori` verifies the committed engine artifacts and
copies the extension to `build/hachidori`. The full app build includes this step,
and Electron packaging puts the result in `resources/hachidori`.

## Local changes

- `extension/overlay-mode.js` enables embedded host behavior. Custom
  JavaScript is disabled because Electron does not provide `userScripts`.
- `extension/subminer-host.js` implements the existing SubMiner popup event and
  command contract and prioritizes character-name results. `content.js` supplies
  popup lifecycle and reader actions.
- `extension/anki-mining.js` marks initial add/overwrite requests for SubMiner's
  AnkiConnect proxy. Later Hachidori pronunciation updates remain unmarked so
  they do not repeat SubMiner media enrichment.
- `extension/anki.js` sends those private markers only to the exact configured
  SubMiner proxy URL. Direct AnkiConnect requests use standard parameters.
- `extension/manifest.json` loads the host bridge and drops `userScripts`.

- External dictionary links retain local Anki templates, audio sources, and custom buttons. Dictionary requests use the host; mining and media rendering use SubMiner. Setup uses Hachidori's native link/unlink messages and verifies the live host inventory.

## Rebuilding the engine

Ordinary SubMiner builds use upstream's committed WASM and JavaScript files,
verified against the SHA-256 checksums in `SOURCE.json`. Frequency annotations
use the existing term-entry API; words without a matching definition entry may
remain unranked. There are no SubMiner C++ or WASM patches.

For an intentional engine rebuild, initialize the nested dependencies with
`git submodule update --init --recursive`, then follow `docs/source-build.md`.
Update the artifact checksums when accepting new engine binaries.

## Updating from upstream

Keep `origin` pointed at this fork and `upstream` at
`https://github.com/bee-san/hachidori.git`. Merge the desired upstream revision
into `subminer`, verify the integration, and update `SOURCE.json`'s upstream
revision, HoshiDicts revision, and artifact checksums as needed. After pushing,
update SubMiner's submodule commit and verify its dictionary integration.

Hachidori and its modifications are GPL-3.0-or-later, see `LICENSE`.
The engine and bundled libraries retain their own license files.
The packaged `extension/vendor/hoshidicts-licenses/` includes dependency and
toolchain notices for the rebuilt engine.
