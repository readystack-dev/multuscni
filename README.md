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

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/multuscni/recipe. The complete kit is the release download. Each release is a tag here.

— ReadyStack · https://readystack.dev
