# creates gobysoft/ubuntu-build-base:24.04.N
# syntax=docker/dockerfile:1
ARG distro=noble
FROM --platform=linux/amd64 ubuntu:${distro}
ARG distro=noble

WORKDIR /root

SHELL ["/bin/bash", "-c"]

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get -y --no-install-recommends install \
            git build-essential ssh cmake gpg gpg-agent \
            devscripts equivs ca-certificates quilt \
            clang clang-tools \
            dput \
            && rm -rf /var/lib/apt/lists/*

ENV CROSS_COMPILE_ARCHS "arm64 armhf"

# Allow us to install packages for cross-compiling architectures
RUN ARCHS=(${CROSS_COMPILE_ARCHS}) && \
    ARCHS_LIST=$(IFS=,; echo "${ARCHS[*]}") && \
    for ARCH in "${ARCHS[@]}"; do dpkg --add-architecture "$ARCH"; done

# Restrict archives.ubuntu.com to amd64
RUN sed -i '/Types: deb/a Architectures: amd64' /etc/apt/sources.list.d/ubuntu.sources 

# Add entry for ports.ubuntu.com
COPY <<EOF /etc/apt/sources.list.d/ubuntu-multiarch.sources
Types: deb
URIs: http://ports.ubuntu.com/
Suites: ${distro} ${distro}-updates ${distro}-backports ${distro}-security
Components: main universe restricted multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
Architectures: ${CROSS_COMPILE_ARCHS}
EOF

# Check that is all works
RUN apt-get update && rm -rf /var/lib/apt/lists/*
