# creates 
# gobysoft/debian-build-arm64-native:12.1 (arm64)
# gobysoft/debian-build-armhf-native:12.1 (armhf)
# docker buildx build --platform=linux/arm64 -t gobysoft/debian-build-arm64-native:12.1 .
# docker buildx build --platform=linux/armhf -t gobysoft/debian-build-armhf-native:12.1 .

FROM debian:bookworm

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
