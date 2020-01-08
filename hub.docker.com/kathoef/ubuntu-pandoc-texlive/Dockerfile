FROM ubuntu:18.04

RUN apt-get update --yes \
 && apt-get install --yes --no-install-recommends \
    texlive-latex-base pandoc \
 && rm -rf /var/lib/apt/lists/*
