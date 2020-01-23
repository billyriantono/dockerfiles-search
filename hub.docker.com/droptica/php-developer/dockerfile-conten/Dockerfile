# target: betflight-dev
FROM ubuntu:16.04
RUN apt-get update && apt-get install -y software-properties-common && \
    add-apt-repository ppa:team-gcc-arm-embedded/ppa && \
    apt-get update && \
    apt-get install -y git gcc-arm-embedded make python gcc clang libblocksruntime-dev && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
