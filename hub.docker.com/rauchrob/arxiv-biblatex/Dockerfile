FROM debian:stretch

RUN apt-get update && apt-get install -y \
    texlive-full \
    biber \
    rubber \
    make \
    latexmk \
    --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*
