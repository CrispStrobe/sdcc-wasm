# sdcc-wasm — SDCC 4.5.0 (mcs51) built for WebAssembly

**This repository is GPL-2.0-or-later. It is not part of any BSD-licensed project.**

It exists for one reason: to distribute the [Small Device C
Compiler](https://sdcc.sourceforge.net/) as WebAssembly, under SDCC's own
licence, separately from applications that merely *use* it. An application can
fetch this toolchain at the user's request without carrying GPL code in its own
distribution.

Served over GitHub Pages at:

    https://crispstrobe.github.io/sdcc-wasm/static/sdcc-wasm/<file>

GitHub Pages sends `Access-Control-Allow-Origin: *`, so a browser on another
origin may fetch and instantiate these modules directly.

## What is here

| file | what it is |
|---|---|
| `static/sdcc-wasm/sdcc.{js,wasm}` | the compiler driver |
| `static/sdcc-wasm/cc1.{js,wasm}` | the C front end |
| `static/sdcc-wasm/sdas8051.{js,wasm}` | the assembler |
| `static/sdcc-wasm/sdld.{js,wasm}` | the linker |
| `static/sdcc-wasm/runtime.json` | packed headers and libraries for the in-memory filesystem |
| `static/sdcc-wasm/include/`, `lib/` | the mcs51 headers and small-model libraries |

SHA-256 of the four binaries:

    a482b8019d48f1f1c02415b0bb274795f5830ffe4b1a93a7e152b9cec8bf8cd2  cc1.wasm
    9c015efff6543e7bfafde2271f1c26ea57984e2f7fdcf6563fa5907827e127e4  sdas8051.wasm
    36c4207dc8a8e8571497cc4b07cae2a3cc98824c289035aa5df8f1e57c47db6d  sdcc.wasm
    d5292272e7ebfbc6dfa5e1cd1c51f1642e11ba7efb3b0c7c3d6f3df23aba55e5  sdld.wasm

## Licence and written offer of source

SDCC is distributed under the **GNU General Public License, version 2 or later**.
The full text is in [`COPYING`](COPYING).

These artifacts are an unmodified build of SDCC 4.5.0, mcs51 port only. The
complete corresponding source is the upstream release tarball:

- **Source:** <https://sourceforge.net/projects/sdcc/files/sdcc/4.5.0/sdcc-src-4.5.0.tar.bz2/download>
- **Source SHA-256:** `d5030437fb436bb1d93a8dbdbfb46baaa60613318f4fb3f5871d72815d1eed80`

No patches were applied to SDCC itself. One build-environment patch was needed
for Emscripten: a `libiberty` `psignal` conflict, resolved by defining
`HAVE_PSIGNAL`. The exact build recipe, toolchain versions and link flags are
recorded in [`BUILD-INFO.md`](BUILD-INFO.md); the workflow that produced them is
`.github/workflows/build-sdcc-wasm.yml` in
[`CrispStrobe/emu8051-stc`](https://github.com/CrispStrobe/emu8051-stc).

As required by GPL-2 section 3, the copyright holder of this distribution offers
to provide the complete corresponding machine-readable source on request, for no
more than the cost of physically performing distribution. Open an issue here.

## The runtime headers carry a linking exception

Each header under `static/sdcc-wasm/include/mcs51/` carries the GPL plus SDCC's
explicit linking exception:

> "As a special exception, if you link this library with other files, some of
> which are compiled with SDCC, to produce an executable, this library does not
> by itself cause the resulting executable to be covered by the GNU General
> Public License. This exception does not however invalidate any other reasons
> why the executable file might be covered by the GNU General Public License."

So a program **compiled with** this toolchain does not inherit GPL obligations
from it. That exception is about the compiler's *output*. It says nothing about
redistributing the compiler itself, which is why this repository is separate.

## Trademarks and affiliation

Not affiliated with, or endorsed by, the SDCC project. SDCC is the work of its
own authors; this repository only rebuilds and redistributes it.
