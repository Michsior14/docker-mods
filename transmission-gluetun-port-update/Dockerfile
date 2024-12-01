FROM ghcr.io/linuxserver/baseimage-alpine:3.20 AS build
ARG MOD_VERSION

RUN \
    if [ -z ${MOD_VERSION+x} ]; then \
    MOD_VERSION=$(curl https://api.github.com/repos/Michsior14/transmission-gluetun-port-update/releases/latest -s | jq .name -r); \
    fi && \
    mkdir -p /root-layer/transmission-gluetun-port-update && \
    curl -o \
    /root-layer/transmission-gluetun-port-update/transmission-gluetun-port-update_x86_64.tar.gz -L \
    "https://github.com/Michsior14/transmission-gluetun-port-update/releases/download/${MOD_VERSION}/transmission-gluetun-port-update_linux_x86_64.tar.gz" && \
    curl -o \
    /root-layer/transmission-gluetun-port-update/transmission-gluetun-port-update_aarch64.tar.gz -L \
    "https://github.com/Michsior14/transmission-gluetun-port-update/releases/download/${MOD_VERSION}/transmission-gluetun-port-update_linux_arm64.tar.gz" && \
    echo "******** run basic test to validate tarballs *********" && \
    for i in x86_64 aarch64; do \
    mkdir -p "/tmp/${i}"; \
    tar xzf "/root-layer/transmission-gluetun-port-update/transmission-gluetun-port-update_${i}.tar.gz" -C "/tmp/${i}"; \
    done
COPY root/ /root-layer/

FROM scratch
COPY --from=build /root-layer/ /