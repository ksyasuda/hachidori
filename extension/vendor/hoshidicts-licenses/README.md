# Dictionary engine notices

These notices accompany the three upstream HoshiDicts WASM runtimes.
`SOURCE.json` in the packaged extension root records the upstream Hachidori and
HoshiDicts revisions and artifact checksums. The corresponding source and rebuild
instructions are in SubMiner's `vendor/hachidori/` submodule.

The engine links Glaze, Zstandard, unordered_dense, libdeflate, utf8proc,
UTF8-CPP, xxHash, lzokay, and gumbo-parser, and uses kanji-processor data.
Each component's original license is included here. Emscripten, musl, libc++,
libc++abi, compiler-rt, and libunwind notices were collected from Emscripten 6.0.9;
this does not identify the toolchain used to build upstream's artifacts.
`reader-and-language-NOTICE` covers upstream reader and
Japanese language adaptations elsewhere in the extension.
