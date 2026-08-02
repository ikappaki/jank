# Changelog

This fork carries Windows-specific changes pending upstream acceptance.
See [README.md](README.md) for context.

Binaries: [jank-win-release](https://github.com/ikappaki/jank-win-release)

## 2026-07-28 (6a74b3c82)

**Synced with:** jank-lang/jank @ [`6a74b3c82`](https://github.com/jank-lang/jank/commit/6a74b3c82ab11212170f14c06f3b1471ef2596ba)
**Changeset:** [main-jank.26-07-28-6a74b3c82...main-win.26-07-28-6a74b3c82](https://github.com/ikappaki/jank-win/compare/main-jank.26-07-28-6a74b3c82...main-win.26-07-28-6a74b3c82)
**Highlight:** Upgrade to LLVM 23 with SEH JITLink, fix char/integer bugs

- Upgrade LLVM from 22 to 23 with SEH JITLink support (`ikappaki/llvm-project@jitlink-coff-seh-llvm-23`)
- Fix `long_long_type()` returning `"long"` instead of `"long long"` (copy-paste bug in overload resolution)
- Fix `(char N)` truncating Unicode code points above U+FFFF on Windows (`wchar_t` → `char32_t`/`c32rtomb`/`mbrtoc32`)
- Fix `_WIN32` preprocessor check in `pass-widen-to-long` test
- Add `JANK_CLJ_TEST_FILTER` env var for running individual clojure-test-suite tests
- Remove `-DGC_NO_THREAD_REDIRECTS` (superseded by upstream [#846](https://github.com/jank-lang/jank/pull/846)/[#888](https://github.com/jank-lang/jank/pull/888))

## 2026-06-19 (56b77d7e9)

**Synced with:** jank-lang/jank @ [`56b77d7e9`](https://github.com/jank-lang/jank/commit/56b77d7e9c555cfc59528124d199dbb54967b2c5)
**Changeset:** [main-jank.26-06-19-56b77d7e9...main-win.26-06-19-56b77d7e9](https://github.com/ikappaki/jank-win/compare/main-jank.26-06-19-56b77d7e9...main-win.26-06-19-56b77d7e9)
**Highlight:** nREPL test suite + fix future deref segfault (GC_NO_THREAD_REDIRECTS)

- Add `-DGC_NO_THREAD_REDIRECTS` to fix `future` deref segfault on macOS ([#813](https://github.com/jank-lang/jank/discussions/813))
- Extend nREPL server with test-support hooks (header + implementation changes)
- Add nREPL test suite: bencode, parsec, connection harness, and core server tests (`test/bash/nrepl-server/`)

## 2026-05-26 (80c2d4f06)

**Synced with:** jank-lang/jank @ [`80c2d4f06`](https://github.com/jank-lang/jank/commit/80c2d4f0672d55d57102d34f5ad328b4ef551329)
**Changeset:** [main-jank.26-05-26-80c2d4f06...main-win.26-05-26-80c2d4f06](https://github.com/ikappaki/jank-win/compare/main-jank.26-05-26-80c2d4f06...main-win.26-05-26-80c2d4f06)
**Highlight:** SEH exception support via custom LLVM build, all Windows exception tests re-enabled

- Switch LLVM to ikappaki/llvm-project (branch `support/jitlink-coff-seh-llvm-22`) for SEH exception support
- Re-enable all Windows exception tests (JIT skip list, bash E2E suites)
- Fix `unsigned long` → `unsigned long long` pointer cast for 64-bit Windows
- Fix negative code point range check in `character.cpp`
- Fix module-path separator in error-reporting tests for Windows
- Add README banner identifying fork purpose
- Add CHANGELOG-WIN.md

