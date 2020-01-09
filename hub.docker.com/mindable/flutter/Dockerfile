FROM ubuntu:latest

LABEL maintainer="team@mindable.health"

WORKDIR /

RUN apt-get update && \
    apt-get install -y lcov git-core curl unzip libglu1 lib32stdc++6 && \
    git clone -b stable --depth=1 https://github.com/flutter/flutter.git && \
    /flutter/bin/flutter doctor && \
    apt-get remove -y curl unzip && \
    apt autoremove -y && \
    rm -rf /var/lib/apt/lists/*

ENV PATH $PATH:/flutter/bin/cache/dart-sdk/bin:/flutter/bin
