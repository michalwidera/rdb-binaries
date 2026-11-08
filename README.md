# rdb-binaries

Prebuilt RetractorDB engine binaries for the artifact package (`rdb-artifact`). They let a reviewer who has only the anonymous mirrors repeat the deterministic measurements of the paper on their own machine, without git and without a compiler (`bin/review.sh --remeasure` in `rdb-artifact`).

## What this repository holds

- `.tar.gz` bundles of `xretractor`, `xqry` and `xtrdb`, one per measurement profile and architecture (`x86_64`, `aarch64`), built in Release with `RDB_BENCH_PROBE` from the pinned engine revision.
- Next to each bundle, the `--build-info` output of every binary in it.

Nothing else: no research data, no sources, no scripts. The research data stay in `rdb-experiment`, the sources in the engine repository, and the procedure in `rdb-artifact`.

## Declaration and its limits

The engine revision, the profile of each bundle and the SHA-256 sum of every archive are declared in `MANIFEST.md` of `rdb-artifact`, which is the only place a reviewer needs to trust. The mirror serves binary files byte for byte, so the sum can be checked after the download.

The sum proves that the reviewer runs the bundle that was declared. It does not prove that the bundle was built from the declared revision: that proof is a build from the pinned sources, which stays the path described in `REPRODUCE.md` of `rdb-artifact`.

## State

No bundles yet. The first ones are added by `bin/build_bundle.sh` of `rdb-artifact` (retractordb #588, step 1).
