FROM ubuntu:18.04

RUN apt-get update \
    && apt-get -y install --no-install-recommends openssh-client make curl git lib32stdc++6 openjdk-8-jdk-headless unzip xz-utils libglu1-mesa \
    && apt-get --purge autoremove \
    && apt-get autoclean \
    && rm -rf /var/lib/apt/lists/*
