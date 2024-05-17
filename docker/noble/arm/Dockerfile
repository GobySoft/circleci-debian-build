# creates 
# gobysoft/ubuntu-build-arm64-native:24.04.1 (arm64)
# gobysoft/ubuntu-build-armhf-native:24.04.1 (armhf)
# docker buildx build --platform=linux/arm64 -t gobysoft/ubuntu-build-arm64-native:24.04.1 .
# docker buildx build --platform=linux/armhf -t gobysoft/ubuntu-build-armhf-native:24.04.1 .

FROM ubuntu:noble
 
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
