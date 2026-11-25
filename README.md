# Multus CNI: ReadyStack build kit

The offline build kit for the Docker image `readystack/multuscni:v4.3.2-CE-ubuntu24.04-r3`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [v4.3.2-CE-ubuntu24.04-r3](https://github.com/readystack-dev/multuscni/releases/tag/v4.3.2-CE-ubuntu24.04-r3)
- Image: [`docker.io/readystack/multuscni:v4.3.2-CE-ubuntu24.04-r3`](https://hub.docker.com/r/readystack/multuscni/tags), manifest digest `sha256:c756394f10bf375ad51f83eda98d3f6a88b5cafebd5c81eaff86fa2d44cb746e`
- Product page: https://readystack.dev/products/multuscni
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=multuscni

Multus CNI is distributed under its upstream licence (Apache-2.0); the kit contains upstream's source under that licence, and each vendored component under its own.

## Download

From the [v4.3.2-CE-ubuntu24.04-r3 release](https://github.com/readystack-dev/multuscni/releases/tag/v4.3.2-CE-ubuntu24.04-r3): `ReadyStack-multuscni-v4.3.2-CE-ubuntu24.04-r3.tar.gz` (437.5 MB), SHA-256 `74a12157d43c1b402709c0089010bcedae8e43995d97117d3c127fda23aeeb2c`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-multuscni-v4.3.2-CE-ubuntu24.04-r3.rebuild.json.sigstore ReadyStack-multuscni-v4.3.2-CE-ubuntu24.04-r3.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-multuscni-v4.3.2-CE-ubuntu24.04-r3.tar.gz
cd v4.3.2-CE-ubuntu24.04-r3
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-multuscni-v4.3.2-CE-ubuntu24.04-r3.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/multuscni/recipe. The complete kit is the release download. Each release is a tag here.
