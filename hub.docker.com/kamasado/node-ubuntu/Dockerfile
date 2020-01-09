FROM ubuntu:18.04

RUN apt-get update && apt-get install -y \
    nodejs \
    npm \
    && npm i -g yarn \
    && rm -rf /var/lib/apt/lists/*
