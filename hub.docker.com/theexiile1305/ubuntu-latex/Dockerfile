FROM ubuntu:18.04

ARG DEBIAN_FRONTEND=noninteractive

RUN set -x;                                       \
    apt-get update -q -y;                         \
    apt-get install -q -y --no-install-recommends \
        build-essential                           \
        texlive-full                              \
        fonts-lato                                \
        latexmk                                   \
        inkscape                                  \
        ;                                         \
    apt-get autoremove -q -y;                     \
    apt-get clean -q -y;                          \
    rm -rf /var/lib/apt/lists/*

