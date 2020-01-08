FROM debian:stable-slim

RUN apt-get update \
  && apt-get install -y libgmp10 \
  && rm -rf /var/lib/apt/lists/*
