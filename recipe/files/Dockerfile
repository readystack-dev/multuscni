# GENERATED L-009 hermetic build (--network=none, SBOM+SLSA-attestation-producing).
# Pinned bases from BASE_IMAGE_DIGESTS.lock; vendored Go tree + debs from Dockerfile.vendor.
FROM golang:1.26.11-bookworm@sha256:dc40a13b61304647ed7e5d581d246b86413dfc29d63c6d018310feb93cd98fc0 AS build_multus
WORKDIR /src
COPY vendored/multuscni-src/ .
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOWORK=off GOFLAGS="-mod=vendor -buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795161129
RUN go build -trimpath -ldflags='-X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.version=v4.3.2 -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.commit=1d81062afcb32eb7290fa28bcbc482c3d0c5cae9 -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.gitTreeState=dirty -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.releaseStatus=,released -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.date=2026-10-21T07:01:58+00:00' -o /multus ./cmd/multus && /multus -version > /tmp/multus.version 2>&1; cat /tmp/multus.version; grep -qF 'version:v4.3.2(dirty,released), commit:1d81062afcb32eb7290fa28bcbc482c3d0c5cae9' /tmp/multus.version || { echo 'multus -version does not report version:v4.3.2(dirty,released), commit:1d81062afcb32eb7290fa28bcbc482c3d0c5cae9'; exit 1; } && \
    { readelf -lW /multus | sed -n 's/.*Requesting program interpreter: \(.*\)]$/\1/p'; readelf -dW /multus | sed -n 's/.*Shared library: \[\(.*\)\]$/\1/p'; } > /multus.needs
FROM golang:1.26.11-bookworm@sha256:dc40a13b61304647ed7e5d581d246b86413dfc29d63c6d018310feb93cd98fc0 AS build_multus-daemon
WORKDIR /src
COPY vendored/multuscni-src/ .
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOWORK=off GOFLAGS="-mod=vendor -buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795161129
RUN go build -trimpath -ldflags='-X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.version=v4.3.2 -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.commit=1d81062afcb32eb7290fa28bcbc482c3d0c5cae9 -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.gitTreeState=dirty -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.releaseStatus=,released -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.date=2026-10-21T07:01:58+00:00' -o /multus-daemon ./cmd/multus-daemon && /multus-daemon -version > /tmp/multus-daemon.version 2>&1; cat /tmp/multus-daemon.version; grep -qF 'version:v4.3.2(dirty,released)' /tmp/multus-daemon.version || { echo 'multus-daemon -version does not report version:v4.3.2(dirty,released)'; exit 1; } && \
    { readelf -lW /multus-daemon | sed -n 's/.*Requesting program interpreter: \(.*\)]$/\1/p'; readelf -dW /multus-daemon | sed -n 's/.*Shared library: \[\(.*\)\]$/\1/p'; } > /multus-daemon.needs
FROM golang:1.26.11-bookworm@sha256:dc40a13b61304647ed7e5d581d246b86413dfc29d63c6d018310feb93cd98fc0 AS build_multus-shim
WORKDIR /src
COPY vendored/multuscni-src/ .
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOWORK=off GOFLAGS="-mod=vendor -buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795161129
RUN go build -trimpath -ldflags='-X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.version=v4.3.2 -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.commit=1d81062afcb32eb7290fa28bcbc482c3d0c5cae9 -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.gitTreeState=dirty -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.releaseStatus=,released -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.date=2026-10-21T07:01:58+00:00' -o /multus-shim ./cmd/multus-shim && /multus-shim -version > /tmp/multus-shim.version 2>&1; cat /tmp/multus-shim.version; grep -qF 'version:v4.3.2(dirty,released)' /tmp/multus-shim.version || { echo 'multus-shim -version does not report version:v4.3.2(dirty,released)'; exit 1; } && \
    { readelf -lW /multus-shim | sed -n 's/.*Requesting program interpreter: \(.*\)]$/\1/p'; readelf -dW /multus-shim | sed -n 's/.*Shared library: \[\(.*\)\]$/\1/p'; } > /multus-shim.needs
FROM golang:1.26.11-bookworm@sha256:dc40a13b61304647ed7e5d581d246b86413dfc29d63c6d018310feb93cd98fc0 AS build_install_multus
WORKDIR /src
COPY vendored/multuscni-src/ .
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOWORK=off GOFLAGS="-mod=vendor -buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795161129
RUN go build -trimpath -ldflags='-X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.version=v4.3.2 -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.commit=1d81062afcb32eb7290fa28bcbc482c3d0c5cae9 -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.gitTreeState=dirty -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.releaseStatus=,released -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.date=2026-10-21T07:01:58+00:00' -o /install_multus ./cmd/install_multus && /install_multus --help 2>&1 | grep -q -- --dest-dir && \
    { readelf -lW /install_multus | sed -n 's/.*Requesting program interpreter: \(.*\)]$/\1/p'; readelf -dW /install_multus | sed -n 's/.*Shared library: \[\(.*\)\]$/\1/p'; } > /install_multus.needs
FROM golang:1.26.11-bookworm@sha256:dc40a13b61304647ed7e5d581d246b86413dfc29d63c6d018310feb93cd98fc0 AS build_thin_entrypoint
WORKDIR /src
COPY vendored/multuscni-src/ .
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOWORK=off GOFLAGS="-mod=vendor -buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795161129
RUN go build -trimpath -ldflags='-X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.version=v4.3.2 -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.commit=1d81062afcb32eb7290fa28bcbc482c3d0c5cae9 -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.gitTreeState=dirty -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.releaseStatus=,released -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.date=2026-10-21T07:01:58+00:00' -o /thin_entrypoint ./cmd/thin_entrypoint && /thin_entrypoint --help 2>&1 | grep -q -- --multus-conf-file && \
    { readelf -lW /thin_entrypoint | sed -n 's/.*Requesting program interpreter: \(.*\)]$/\1/p'; readelf -dW /thin_entrypoint | sed -n 's/.*Shared library: \[\(.*\)\]$/\1/p'; } > /thin_entrypoint.needs
FROM golang:1.26.11-bookworm@sha256:dc40a13b61304647ed7e5d581d246b86413dfc29d63c6d018310feb93cd98fc0 AS build_kubeconfig_generator
WORKDIR /src
COPY vendored/multuscni-src/ .
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOWORK=off GOFLAGS="-mod=vendor -buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795161129
RUN go build -trimpath -ldflags='-X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.version=v4.3.2 -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.commit=1d81062afcb32eb7290fa28bcbc482c3d0c5cae9 -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.gitTreeState=dirty -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.releaseStatus=,released -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.date=2026-10-21T07:01:58+00:00' -o /kubeconfig_generator ./cmd/kubeconfig_generator && /kubeconfig_generator --help 2>&1 | grep -q -- --bootstrap-config && \
    { readelf -lW /kubeconfig_generator | sed -n 's/.*Requesting program interpreter: \(.*\)]$/\1/p'; readelf -dW /kubeconfig_generator | sed -n 's/.*Shared library: \[\(.*\)\]$/\1/p'; } > /kubeconfig_generator.needs
FROM golang:1.26.11-bookworm@sha256:dc40a13b61304647ed7e5d581d246b86413dfc29d63c6d018310feb93cd98fc0 AS build_cert-approver
WORKDIR /src
COPY vendored/multuscni-src/ .
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOWORK=off GOFLAGS="-mod=vendor -buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795161129
RUN go build -trimpath -ldflags='-X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.version=v4.3.2 -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.commit=1d81062afcb32eb7290fa28bcbc482c3d0c5cae9 -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.gitTreeState=dirty -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.releaseStatus=,released -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.date=2026-10-21T07:01:58+00:00' -o /cert-approver ./cmd/cert-approver && /cert-approver 2>&1 | grep -q 'starting cert-approver' && \
    { readelf -lW /cert-approver | sed -n 's/.*Requesting program interpreter: \(.*\)]$/\1/p'; readelf -dW /cert-approver | sed -n 's/.*Shared library: \[\(.*\)\]$/\1/p'; } > /cert-approver.needs
FROM golang:1.26.11-bookworm@sha256:dc40a13b61304647ed7e5d581d246b86413dfc29d63c6d018310feb93cd98fc0 AS build_passthru
WORKDIR /src
COPY vendored/multuscni-src/ .
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOWORK=off GOFLAGS="-mod=vendor -buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795161129
RUN go build -trimpath -ldflags='-X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.version=v4.3.2 -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.commit=1d81062afcb32eb7290fa28bcbc482c3d0c5cae9 -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.gitTreeState=dirty -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.releaseStatus=,released -X gopkg.in/k8snetworkplumbingwg/multus-cni.v4/pkg/multus.date=2026-10-21T07:01:58+00:00' -o /passthru ./cmd/passthru-cni && /passthru 2>&1 | grep -q 'Passthrough CNI Plugin' && \
    { readelf -lW /passthru | sed -n 's/.*Requesting program interpreter: \(.*\)]$/\1/p'; readelf -dW /passthru | sed -n 's/.*Shared library: \[\(.*\)\]$/\1/p'; } > /passthru.needs
# rs-probe: the HEALTHCHECK helper (standard library only, from the kit's rs-probe.go)
FROM golang:1.26.11-bookworm@sha256:dc40a13b61304647ed7e5d581d246b86413dfc29d63c6d018310feb93cd98fc0 AS build_rs_probe
WORKDIR /probe
COPY rs-probe.go main.go
COPY rs-probe.mod go.mod
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOFLAGS="-buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795161129
RUN go build -trimpath -ldflags='-s -w' -o /rs-probe .
# the chiselled rootfs (vendored/chisel, cut by Dockerfile.vendor), the service user, the binaries
FROM ubuntu:24.04@sha256:9c7f200c07e3d4a03e7249d2c16bf66a51120fb876aa2242cf31451412543289 AS rootfs
ARG SOURCE_DATE_EPOCH=1795161129
ADD vendored/chisel/rootfs.tar /rootfs/
RUN printf 'multuscni:x:999:999::/var/lib/multuscni:/bin/sh\n' >> /rootfs/etc/passwd && printf 'multuscni:x:999:\n' >> /rootfs/etc/group && \
    mkdir -p /rootfs/var/lib/multuscni && chown -R 999:999 /rootfs/var/lib/multuscni
COPY --from=build_multus /multus /rootfs/usr/src/multus-cni/bin/multus
COPY --from=build_multus /multus.needs /tmp/needs/multus
COPY --from=build_multus-daemon /multus-daemon /rootfs/usr/src/multus-cni/bin/multus-daemon
COPY --from=build_multus-daemon /multus-daemon.needs /tmp/needs/multus-daemon
COPY --from=build_multus-shim /multus-shim /rootfs/usr/src/multus-cni/bin/multus-shim
COPY --from=build_multus-shim /multus-shim.needs /tmp/needs/multus-shim
COPY --from=build_install_multus /install_multus /rootfs/usr/src/multus-cni/bin/install_multus
COPY --from=build_install_multus /install_multus.needs /tmp/needs/install_multus
COPY --from=build_thin_entrypoint /thin_entrypoint /rootfs/usr/src/multus-cni/bin/thin_entrypoint
COPY --from=build_thin_entrypoint /thin_entrypoint.needs /tmp/needs/thin_entrypoint
COPY --from=build_kubeconfig_generator /kubeconfig_generator /rootfs/usr/src/multus-cni/bin/kubeconfig_generator
COPY --from=build_kubeconfig_generator /kubeconfig_generator.needs /tmp/needs/kubeconfig_generator
COPY --from=build_cert-approver /cert-approver /rootfs/usr/src/multus-cni/bin/cert-approver
COPY --from=build_cert-approver /cert-approver.needs /tmp/needs/cert-approver
COPY --from=build_passthru /passthru /rootfs/usr/src/multus-cni/bin/passthru
COPY --from=build_passthru /passthru.needs /tmp/needs/passthru
COPY --from=build_rs_probe /rs-probe /rootfs/usr/local/bin/rs-probe
COPY --from=build_install_multus /install_multus /rootfs/install_multus
COPY --from=build_thin_entrypoint /thin_entrypoint /rootfs/thin_entrypoint
COPY --from=build_kubeconfig_generator /kubeconfig_generator /rootfs/kubeconfig_generator
COPY --from=build_cert-approver /cert-approver /rootfs/cert-approver
COPY --from=build_multus /src/LICENSE /rootfs/usr/src/multus-cni/LICENSE
RUN chmod 755 /rootfs/usr/src/multus-cni/bin/multus /rootfs/usr/src/multus-cni/bin/multus-daemon /rootfs/usr/src/multus-cni/bin/multus-shim /rootfs/usr/src/multus-cni/bin/install_multus /rootfs/usr/src/multus-cni/bin/thin_entrypoint /rootfs/usr/src/multus-cni/bin/kubeconfig_generator /rootfs/usr/src/multus-cni/bin/cert-approver /rootfs/usr/src/multus-cni/bin/passthru /rootfs/usr/local/bin/rs-probe
RUN --mount=type=bind,source=vendored/chisel,target=/chisel set -eu; \
    for n in /tmp/needs/*; do while read -r lib; do [ -n "$lib" ] || continue; \
      case "$lib" in /*) [ -e "/rootfs$lib" ] ;; *) [ -n "$(find /rootfs/usr/lib /rootfs/usr/lib64 -name "$lib" 2>/dev/null | head -1)" ] ;; esac || \
      { echo "$(basename "$n") needs $lib, which the chiselled rootfs does not have: add its slice to runtime_base.slices" >&2; exit 1; }; \
    done < "$n"; done; rm -rf /tmp/needs; \
    [ -e /rootfs/etc/os-release ] || { echo "no /etc/os-release: base-files_release-info is missing" >&2; exit 1; }; \
    [ "$(grep -c '^Package: ' /rootfs/var/lib/dpkg/status)" = "$(wc -l < /chisel/packages.tsv)" ] || \
      { echo "/var/lib/dpkg/status does not list every package of vendored/chisel/packages.tsv" >&2; exit 1; }; \
    rm -rf /rootfs/var/log/dpkg.log /rootfs/var/log/alternatives.log /rootfs/var/log/apt /rootfs/var/cache/ldconfig/aux-cache /rootfs/var/cache/fontconfig
FROM scratch
ARG SOURCE_DATE_EPOCH=1795161129
COPY --from=rootfs /rootfs/ /
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
LABEL org.opencontainers.image.licenses="Apache-2.0"
LABEL org.opencontainers.image.title="Multus CNI"
LABEL org.opencontainers.image.source="https://github.com/k8snetworkplumbingwg/multus-cni"
LABEL org.opencontainers.image.version="v4.3.2-CE-ubuntu24.04-r3"
LABEL org.opencontainers.image.revision="1d81062afcb32eb7290fa28bcbc482c3d0c5cae9"
# image_healthcheck false: no HEALTHCHECK (a Kubernetes pod component; the kubelet ignores one)
WORKDIR /
USER multuscni
ENTRYPOINT ["/thin_entrypoint"]
