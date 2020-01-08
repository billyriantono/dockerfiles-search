FROM debian:jessie-slim

RUN apt-get update -y && apt-get install -y \
    openssh-client \
    --no-install-recommends && rm -r /var/lib/apt/lists/*
