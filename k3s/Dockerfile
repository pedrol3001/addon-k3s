
ARG BUILD_FROM=ghcr.io/hassio-addons/debian-base/amd64:7.3.3

# hadolint ignore=DL3006
FROM ${BUILD_FROM}
ARG BUILD_ARCH

ARG K3S_VERSION=v1.29.3+k3s1

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

ENV INSTALL_K3S_VERSION=${K3S_VERSION}
ENV INSTALL_K3S_SKIP_ENABLE=true
ENV INSTALL_K3S_SKIP_START=true

# hadolint ignore=DL3008
RUN apt-get update \
    && apt-get install -y --no-install-recommends curl systemd \
    && curl -sfL https://get.k3s.io | sh -s - --docker \
    && rm -fr  \
        /tmp/* \
        /var/{cache,log}/* \
        /var/lib/apt/lists/*

# Copy root filesystem
COPY rootfs /

EXPOSE 2379 2380 6443 8472/udp 10250 51820/udp 51821/udp 5001

# Build arguments
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Pedro Luis <contact@pedrol.me>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Home Assistant K3S Add-on" \
    org.opencontainers.image.authors="Pedro Luis <contact@pedrol.me>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://addons.community" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
