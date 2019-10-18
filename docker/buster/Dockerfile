# creates gobysoft/debian-build-base:10.N
FROM debian:buster
 
WORKDIR /root

SHELL ["/bin/bash", "-c"]

RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get -y --no-install-recommends install \
            git build-essential ssh cmake gpg gpg-agent \
            devscripts equivs ca-certificates quilt \
            && rm -rf /var/lib/apt/lists/*

ENV CROSS_COMPILE_ARCHS "arm64 armhf"

# Allow us to install packages for cross-compiling architectures
RUN ARCHS=(${CROSS_COMPILE_ARCHS}) && \
    for ARCH in "${ARCHS[@]}"; do dpkg --add-architecture "$ARCH"; done
