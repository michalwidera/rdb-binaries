# rdb-binaries

Prebuilt RetractorDB engine binaries for the artifact package (`rdb-artifact`). They let a reviewer who has only the anonymous mirrors repeat the deterministic measurements of the paper on their own machine, without git and without a compiler (`bash bin/review.sh --remeasure` in `rdb-artifact`).

## What this repository holds

One directory per engine revision, named by its full SHA. In it, one `.tar.gz` bundle per measurement profile and architecture:

```
<engine SHA>/
  rdb-<sha12>-h9-<PROFILE>-linux-<x86_64|aarch64>.tar.gz              bin/xretractor, bin/xqry, bin/xtrdb, build-info.txt, BUILD.txt
  rdb-<sha12>-h9-<PROFILE>-linux-<x86_64|aarch64>.build-info.txt      the bundle's build-info.txt, readable without unpacking
  SHA256SUMS
```

The profiles are the four of the H9 campaign (`rdb-experiment/results_20261103_R593_H9/profiles.tsv`): `DEFAULT`, `NO_R2_CANON`, `NO_R1_FACTOR` and `NO_R1_NO_R2`. Every binary is a Release build with `RDB_BENCH_PROBE=ON`, made by `bin/build_bundle.sh` of `rdb-artifact` inside the image of the engine's `packaging/portable/Dockerfile` (Debian 13, GCC 14.2.0). Running the binaries needs Linux with glibc 2.38 or later and the libstdc++ of GCC 14 or later (Debian 13, Ubuntu 24.04).

Nothing else: no research data, no sources, no scripts. The research data stay in `rdb-experiment`, the sources in the engine repository, and the procedure in `rdb-artifact`.

## Declaration and its limits

The engine revision, the profile of each bundle and the SHA-256 sum of every archive are declared in `MANIFEST.md` of `rdb-artifact` (section 7), which is the only place a reviewer needs to trust; `SHA256SUMS` here is a convenience copy. The mirror serves binary files byte for byte, so the sum can be checked after the download.

The sum proves that the reviewer runs the bundle that was declared. It does not prove that the bundle was built from the declared revision: that proof is a build from the pinned sources, which stays the path described in `REPRODUCE.md` of `rdb-artifact`.
