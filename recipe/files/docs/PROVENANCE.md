# Provenance — Multus CNI (`v4.3.2-CE-ubuntu24.04-r3`)

Every item below is copied from a record in this archive; the record is named in brackets.

## Source

- Upstream repository: https://github.com/k8snetworkplumbingwg/multus-cni
- Revision built: `v4.3.2` (commit `1d81062afcb32eb7290fa28bcbc482c3d0c5cae9`)
- Source tree: `e0f3ab4e4ec869c7bcc00c31d2acf5a075aee8ef7e25ee5783bc99b188105722` over 159 files [`docs/provenance/SOURCE_TREE_HASH.json`]
- Community Edition only: enterprise code is removed or refused before the build (CE audit at acquire).

## Build

- Method: `source-rebuild-go`; base image `scratch + a chiselled Ubuntu 24.04 runtime (vendored/chisel/slices.txt, packages.tsv)`
- Compiled with `--network=none` from vendored source, dependencies and base images; BuildKit pinned to `moby/buildkit:v0.31.2` (shipped in `toolchain/`).
- SOURCE_DATE_EPOCH: `1795161129` [`SOURCE_DATE_EPOCH.txt`]
- Frozen inputs: [`docs/provenance/FREEZE_MANIFEST.json`], build recipe: [`docs/provenance/BUILD_RECIPE.json`].

## Output

- Published image: `readystack/multuscni:v4.3.2-CE-ubuntu24.04-r3` — index digest `sha256:ba303d9c11b4b94d729d45320b8a58bdee68237f8eed333bb57f9202d7cc65da` [`docs/provenance/LOCKED_DIGEST.txt`]
- linux/amd64 image digest `sha256:c756394f10bf375ad51f83eda98d3f6a88b5cafebd5c81eaff86fa2d44cb746e` — reproduced from this archive before publishing [`docs/provenance/REPRO_VERIFICATION.json`].

## Attestations and signature

- SBOM + SLSA provenance attached to the image: attached: an SPDX SBOM and SLSA v1 provenance [`docs/provenance/SCOUT_VERDICT.json`]
- cosign signature by the ReadyStack release key: verified before publishing. Check it: `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/multuscni:v4.3.2-CE-ubuntu24.04-r3`

## Pinned inputs, and why

- 25 pinned inputs, each with where it came from, why this one, how it was checked and when it was decided: `docs/PINS.md` [`docs/provenance/PINS.json`] (upstream source 2, base and build images 3, image digests 2, dependency versions readystack sets 3, pins in the kit's dockerfiles 8, readystack's build engine 5, dependencies upstream chose 2).

## Build trail

- How this release passed through the ReadyStack harness, record by record (every chain, drive, stage, review round, defect and check, each naming the record it is copied from): `ReadyStack-multuscni-v4.3.2-CE-ubuntu24.04-r3.trail.json`, published beside this archive and signed with the release key (`ReadyStack-multuscni-v4.3.2-CE-ubuntu24.04-r3.trail.json.sigstore`), and readable at https://readystack.dev/products/multuscni/trail/v4.3.2-CE-ubuntu24.04-r3.

