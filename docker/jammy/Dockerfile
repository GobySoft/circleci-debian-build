# creates gobysoft/ubuntu-build-base:22.04.N
FROM ubuntu:jammy
 
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
    for ARCH in "${ARCHS[@]}"; do dpkg --add-architecture "$ARCH"; done && \
    sed -i 's/deb /deb [arch=amd64] /' /etc/apt/sources.list && \
    egrep "^deb " /etc/apt/sources.list | sed "s/amd64/${ARCHS_LIST}/" \
        | sed 's|http://.*.ubuntu.com/ubuntu/|http://ports.ubuntu.com/|' \
        >> /etc/apt/sources.list
