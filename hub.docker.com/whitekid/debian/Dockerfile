FROM debian:stretch

RUN apt update && \
    apt install -y --no-install-recommends \
      ca-certificates \
      curl \
    && \
    rm -rf /var/lib/apt/lists/*
