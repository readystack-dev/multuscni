[![ReadyStack](https://readystack.dev/logo.svg)](https://readystack.dev)

**Stable, Open-source Releases, Automated** · [readystack.dev](https://readystack.dev)

[![Docker Hub](https://img.shields.io/badge/Docker%20Hub-readystack%2Fmultuscni-2496ED?logo=docker&logoColor=white)](https://hub.docker.com/r/readystack/multuscni) [![Docker pulls](https://img.shields.io/docker/pulls/readystack/multuscni)](https://hub.docker.com/r/readystack/multuscni) [![Grade at release](https://img.shields.io/badge/grade%20at%20release-A%20%2894%25%29-2ea44f)](https://readystack.dev/products/multuscni) [![Signed: cosign](https://img.shields.io/badge/signed-cosign-2ea44f)](https://readystack.dev/keys/cosign.pub) ![SBOM: SPDX](https://img.shields.io/badge/SBOM-SPDX-2ea44f) ![Provenance: SLSA v1](https://img.shields.io/badge/provenance-SLSA%20v1-2ea44f) ![Offline rebuild: verified](https://img.shields.io/badge/offline%20rebuild-verified-2ea44f)

# Multus CNI: ReadyStack build kit

The offline build kit for the Docker image `readystack/multuscni:v4.3.2-CE-ubuntu24.04-r3`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [v4.3.2-CE-ubuntu24.04-r3](https://github.com/readystack-dev/multuscni/releases/tag/v4.3.2-CE-ubuntu24.04-r3)
- Image: [`docker.io/readystack/multuscni:v4.3.2-CE-ubuntu24.04-r3`](https://hub.docker.com/r/readystack/multuscni/tags), manifest digest `sha256:c756394f10bf375ad51f83eda98d3f6a88b5cafebd5c81eaff86fa2d44cb746e`
- Product page: https://readystack.dev/products/multuscni
- Source and build recipe: https://readystack.dev/products/multuscni/recipe
- Build trail: https://readystack.dev/products/multuscni/trail/v4.3.2-CE-ubuntu24.04-r3
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=multuscni

## The image

The kube-multus DaemonSet (product-kits/kubevirt-stack/install/network/multus-daemonset.yml, upstream's deployments/multus-daemonset.yml with our image): init container /install_multus --type thin, then /thin_entrypoint --multus-conf-file=auto --multus-autoconfig-dir=/host/etc/cni/net.d --cni-conf-dir=/host/etc/cni/net.d. The image's default user is the unprivileged multuscni (uid 999); both containers set runAsUser: 0, because they write the host's root-owned /etc/cni/net.d and /opt/cni/bin, and only the init container install-multus-binary also sets privileged: true (upstream also sets it on kube-multus; the bundle drops it there, since root's default capabilities are enough).

## Who uses Multus CNI and why

Kubernetes operators whose pods need more than one network interface, for example to reach a separate storage or management network.

Multus CNI lets a pod have several network interfaces. It acts as a meta-plugin, calling other CNI plugins to attach extra networks alongside the cluster's default pod network.

A typical use: A team runs workloads that must also sit on a separate VLAN. With Multus, each pod keeps its normal interface on the cluster network and gets an additional interface on the VLAN, described in a network attachment definition and created by another CNI plugin.

From the upstream project's own description: https://github.com/k8snetworkplumbingwg/multus-cni.

## This release

- Docker Scout policy grade at release: **A** (94%), graded 2026-11-20 with `docker scout policy` (CLI 1.26.0, docker-default configuration).
  - Docker Scout counts 7 packages with copyleft licences (GPL, LGPL, MPL), all of them operating-system packages (it counts only packages whose licence it can read; the SBOM lists every component).
- Signed with ReadyStack's release key (fingerprint `04daa92344a52dbc`): https://readystack.dev/keys/cosign.pub.
- Runs as a non-root user (`multuscni`).
- Attestations on the image: an SPDX SBOM and SLSA provenance v1.
- Rebuilt from this kit with network egress blocked on 2026-11-20; the rebuilt image digest is the published one.
- Base: Ubuntu 24.04.

The current grade, measured again every day, is on https://readystack.dev/products/multuscni.

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

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/multuscni/recipe. The complete kit is the release download. Each release is a tag here. How to report a vulnerability: [SECURITY.md](SECURITY.md).

## About ReadyStack

**Stable, Open-source Releases, Automated.** ReadyStack releases popular open-source apps every week with every available critical and high security fix applied, plus full documentation, reference data, tests and a build recipe that recreates each release bit-for-bit. Each release is rebuilt from its pinned inputs with the network off, checked against its published digest, signed, and scanned and graded again every day. The images and build kits are free, and ReadyStack is soon to be a nonprofit.

[readystack.dev](https://readystack.dev) · [All products](https://readystack.dev/products.html) · [Build kits on GitHub](https://github.com/readystack-dev) · [Defect log](https://readystack.dev/defects.html) · contact@readystack.dev

— ReadyStack · https://readystack.dev
