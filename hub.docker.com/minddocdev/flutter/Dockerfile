# ------------------------------------------------------
#                       Dockerfile
# ------------------------------------------------------
# image:    flutter
# name:     minddocdev/flutter
# repo:     https://github.com/minddocdev/flutter
# Requires: ubuntu:latest
# authors:  development@minddoc.com
# ------------------------------------------------------
FROM ubuntu:18.04

LABEL maintainer="development@minddoc.com"

ARG VERSION=v1.9.1+hotfix.2

ENV FLUTTER_PATH=/flutter/bin

WORKDIR /

RUN apt-get update &&\
 apt-get install -y lcov git-core curl unzip libglu1 lib32stdc++6 &&\
 git clone --branch ${VERSION} --depth=1 https://github.com/flutter/flutter.git &&\
 ${FLUTTER_PATH}/flutter doctor &&\
 apt-get remove -y curl unzip &&\
 apt autoremove -y &&\
 rm -rf /var/lib/apt/lists/*

ENV PATH $PATH:${FLUTTER_PATH}/cache/dart-sdk/bin:${FLUTTER_PATH}
