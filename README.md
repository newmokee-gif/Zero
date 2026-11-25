# Zero OS · Zero · Ezero

An experimental operating system, an original self-hosted language and compiler,
and an easier language built on Zero. Project implementations are written in
**Zero or Ezero**, with original internal formats and tools.

**License: GNU GPL version 3 only (GPL-3.0-only).** The project owner has licensed
the original project source and distributed programs under GPLv3. See [LICENSE](LICENSE).
The official license text is also available in our own [LICENSE.ztext](LICENSE.ztext).

## Download

Use the [release page](https://github.com/newmokee-gif/Zero/releases/tag/v0.15.0-preview.1)
for the system image, native Linux/Windows kits, guest programs and complete
corresponding source. The release is a preview, not a production-ready system.

| Download | Purpose |
| --- | --- |
| `zero-os-0.14.zmedia` | Own system-media container, written with Zero Flash |
| `zero-os-0.14.iso` | BIOS/UEFI optical compatibility image for a virtual machine |
| `zero-native-linux-x64-0.15.zpack` | All native Linux programs, Zero/Ezero compilers and libraries |
| `zero-native-windows-x64-0.15.zpack` | All native Windows programs, Zero/Ezero compilers and libraries |
| `zero-programs-0.15.zpack` | Guest compiler/reader applications and UEFI utilities |
| `zero-web-source-0.15-preview.zpack` | Complete corresponding source, seed and own tests |
| `zero-archive` / `zero-archive.exe` | Standalone original unpacker for the `.zpack` downloads |
| `zero-text` / `zero-text.exe` | Standalone original reader for `.ztext` documentation |

On Linux, make the downloaded unpacker executable. Extract into a **new single
directory name in the current directory**, preserving its `lib` subdirectory:

```console
chmod +x zero-archive
./zero-archive read zero-native-linux-x64-0.15.zpack zero-tools
cd zero-tools
./zero-text read README.ztext
./zero examples/hello.zero hello
./hello
./ezero examples/hello.ezero easy-hello
./easy-hello
```

On Windows, use the corresponding `.exe` programs and Windows kit:

```console
zero-archive.exe read zero-native-windows-x64-0.15.zpack zero-tools
cd zero-tools
zero-text.exe read README.ztext
zero.exe examples/hello.zero hello.exe
hello.exe
ezero.exe examples/hello.ezero easy-hello.exe
easy-hello.exe
```

The packaged `zero` is a file-to-file compiler CLI. The `zero` emitted by a raw
project build is a different entry point that reads source from standard input;
the kits include it separately as `zero-native-compiler` (`.exe` on Windows).
Keep the companion libraries together with the packaged compilers.

## Current scope

The system has original x86 BIOS/UEFI32/64 boot paths, a monolithic kernel,
terminal and bounded disk files, bundled Zero/Ezero compilers, a graphical
desktop, an editor and a bounded HTTP text reader. The media tools use the own
`.zmedia`, `.zpack`, `.ztext` and `.zpix` formats and original implementations.

The new **Zero Web 0.15 preview** is a Linux/Windows local-document viewer with
an HTML tree, a CSS subset, a bounded JavaScript interpreter, own pixel renderer
and a native window. Run `zero-web demo.ztext` inside the native kit. It is not
yet installed into the running Zero OS kernel. The supplied system image retains
the verified 0.14 boot/kernel payload.

This is **not** a complete Chromium rewrite or an all-sites browser. The new
engine has no URL fetching, TLS/HTTPS, complete HTML5/ECMAScript, flex/grid,
external scripts/styles or multimedia. It uses an ASCII bitmap font. Website
server-side Python does not require a Python interpreter in the browser; no
Python implementation or runtime is shipped in this project.

Full physical Wi-Fi support, general Btrfs/NTFS/ext4 read/write, process isolation,
SMP and broad hardware compatibility must not be inferred from plans or historical
notes. Current limitations are documented in `WORKSTATE.ztext` and module docs.

## Build and verify

From a native kit, the original builder consumes this repository and writes a
new output directory:

```console
zero-build PROJECT_DIRECTORY NEW_BUILD_DIRECTORY
```

It uses the included original compiler seed and checks its self-hosted fixed
point. The current build produces **72 artifacts in 76 stages**. It does not
invoke a foreign compiler, assembler, linker or shell. Read `tools/build.ztext`
with `zero-text` for the raw compiler entry point and full build contracts.

All new document-engine implementation and project tests are Zero. DOM170,
CSS151, JavaScript320 and integration35 checks pass on Linux and Windows binaries
under Wine. Independent checks cover CLI, formats, composition, renderer bounds,
scrolling and GUI pixels. Rebuilding with the freshly built builder reproduced
all 72 artifacts byte-for-byte. These are bounded test results, not a guarantee
of perfect behavior.

Boot validation for the unchanged system payload was performed in QEMU across
BIOS/UEFI32/64. Native Windows hardware, physical flash drives and VirtualBox are
not newly verified by this release. Wine and QEMU are external test tools and are
not bundled implementations. Private data disks and personal correspondence are
excluded from the public source package.

Development rules: [AGENTS.md](AGENTS.md). Detailed documentation uses the own
`.ztext` format; use `zero-text read FILE.ztext`. The Markdown README and official
license are publication metadata, not additional implementation languages.
