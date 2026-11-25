# Multus CNI v4.3.2 — ReadyStack release `v4.3.2-CE-ubuntu24.04-r3`

Generated 2026-11-20 from this release's build records and strategy. Statements that come from a single record name it in brackets; the others come from this release's strategy and build log.

## Release

- **Image:** `readystack/multuscni:v4.3.2-CE-ubuntu24.04-r3` (linux/amd64). Index digest `sha256:ba303d9c11b4b94d729d45320b8a58bdee68237f8eed333bb57f9202d7cc65da` [`docs/provenance/LOCKED_DIGEST.txt`].
- **Image manifest digest:** `sha256:c756394f10bf375ad51f83eda98d3f6a88b5cafebd5c81eaff86fa2d44cb746e` [`TARGET_DIGEST.txt`].
- **Upstream:** Multus CNI v4.3.2 built from source at `v4.3.2` of https://github.com/k8snetworkplumbingwg/multus-cni — upstream notes: https://github.com/k8snetworkplumbingwg/multus-cni/releases/tag/v4.3.2 [`docs/provenance/BUILD_RECIPE.json`].
- **Base image:** none (`FROM scratch`): a chiselled Ubuntu 24.04 runtime, the files Canonical's chisel cut from Ubuntu's own packages (`vendored/chisel/slices.txt`, `vendored/chisel/packages.tsv`); runtime user `multuscni`.
- **Build:** `source-rebuild-go`, compiled offline with `--network=none`.
- **Supersedes:** ReadyStack release `v4.3.2-CE-ubuntu24.04-r2`.

## What changed in this release

- Upstream version unchanged (v4.3.2); ReadyStack rebuild.
- Minimum dependency versions ReadyStack enforces on top of upstream (raised only where upstream's own version was lower); shipped versions from the SBOM [`docs/sbom/SBOM.json`]:
  - `golang.org/x/net` raised from upstream's `v0.58.0` to at least `v0.62.0` (shipped: `v0.62.0`)
  - `golang.org/x/text` at least `v0.41.0`: not raised, upstream already pins `v0.41.0` (shipped: `v0.43.0`)
  - `google.golang.org/grpc` at least `v1.83.2`: not raised, upstream already pins `v1.83.2` (shipped: `v1.83.2`)
- Multus CNI v4.3.2 is unchanged from the release this supersedes (v4.3.2-CE-ubuntu24.04-r2); this release rebuilds it. Changes: the image is rebuilt on the current ubuntu:24.04 image (sha256:9c7f200c07e3…), which its maintainers updated after v4.3.2-CE-ubuntu24.04-r2 was built on sha256:2198e4c65076…. Settings, ports and data volumes are those of v4.3.2-CE-ubuntu24.04-r2: replace the container with this image on the same volumes.

## Security status at release (measured 2026-11-20)

- **Docker Scout:** 0 fixable critical/high vulnerabilities; runs as `multuscni` (non-root); SBOM + provenance attestations present (SPDX SBOM + SLSA v1) [`docs/provenance/SCOUT_VERDICT.json`].
- **OSV cross-check:** no fixable critical/high vulnerability beyond Docker Scout's findings.
- **Signature:** cosign signature verified by ReadyStack's release gate before publishing; check it yourself with `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/multuscni:v4.3.2-CE-ubuntu24.04-r3` (signatures are recorded in the public Sigstore transparency log).
- **ReadyStack release check at release:** passed (ReadyStack's own test, not a Docker Scout grade). Vulnerabilities are disclosed every day and the image never changes, so it is re-checked daily, beside Docker Scout's own dated grade, at https://readystack.dev/queue.

## Reproducibility

Rebuilds offline from this archive to the identical image digest `sha256:c756394f10bf375ad51f83eda98d3f6a88b5cafebd5c81eaff86fa2d44cb746e`: run `./BUILD_OFFLINE.sh`, then `./VERIFY_OFFLINE.sh` (add `--online` to confirm the Docker Hub tag holds the same digest). Before publishing, ReadyStack rebuilt the kit with `./BUILD_OFFLINE.sh` and compared the result with the published digest [`docs/provenance/REPRO_VERIFICATION.json`], then ran `./BUILD_OFFLINE.sh` and `./VERIFY_OFFLINE.sh` from this archive (without `--online`).

## Validation

- 6 of 6 runbook checks passed (6 authored) on the stack's 3-node integration cluster, recorded 2026-10-29T02:34:55Z [`docs/validation/test-results.json`, from the run's record `docs/stack/RUNBOOK_EVIDENCE.json`]. They are the checks of the stack's operator runbook that name this component; no container of this image was started on its own for them. The record does not show this release's image (`sha256:c756394f10bf375ad51f83eda98d3f6a88b5cafebd5c81eaff86fa2d44cb746e`) in that run: it lists the component's images as they were then, an earlier build or a tag, so the checks describe the component, not this digest.
- Failed cases are listed in `docs/validation/FAILED_TESTS.md`.

## Known issues

- **low** (ReadyStack package): Admin handbook: Parenthetical names the v4.3.1 tag as the name images.tsv gives 'it' (this v4.3.2 image). [`RSD-multuscni-270a997488`] (carried from `v4.3.2-CE-ubuntu24.04-r1`, recorded there as `RSD-multuscni-a5109c973e`)
- **low** (ReadyStack package): Admin handbook: Handbook states images.tsv gives the r2 tag; the repo bundle's images.tsv lists r1. [`RSD-multuscni-4a9e68d8a9`] (carried from `v4.3.2-CE-ubuntu24.04-r2`, recorded there as `RSD-multuscni-65339a0bdc`)

## Verify this archive

```
sha256sum -c CHECKSUMS.sha256
./BUILD_OFFLINE.sh && ./VERIFY_OFFLINE.sh --online
cosign verify --key https://readystack.dev/keys/cosign.pub readystack/multuscni:v4.3.2-CE-ubuntu24.04-r3
```

ReadyStack records every signature in the public Sigstore transparency log (Rekor), so the command needs no extra flags.

