# creates gobysoft/pbuilder-dist-build-base:18.04.N
FROM ubuntu:bionic

WORKDIR /root

SHELL ["/bin/bash", "-c"]

RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get -y --no-install-recommends install \
            ubuntu-dev-tools qemu-user-static binfmt-support pbuilder debian-archive-keyring \
            && rm -rf /var/lib/apt/lists/*

ENV CROSS_COMPILE_ARCHS "arm64 armhf"
ENV CROSS_COMPILE_DISTROS "xenial bionic stretch"

# Allow us to install packages for cross-compiling architectures
RUN ARCHS=(${CROSS_COMPILE_ARCHS}) && \
    DISTROS=(${CROSS_COMPILE_DISTROS}) && \
    for ARCH in "${ARCHS[@]}"; do \
        for DISTRO in "${DISTROS[@]}"; do \
        pbuilder-dist ${DISTRO} ${ARCH} create || exit; \
        done; \
    done
