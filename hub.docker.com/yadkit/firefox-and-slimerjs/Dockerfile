FROM ubuntu:18.04
RUN apt-get update && apt-get install --no-install-recommends -y \
      htop \
      curl \
      wget \
      nano \
      ca-certificates \
      firefox='59.*' \
      npm \
      jq \
    && rm -rf /var/lib/apt/lists/*
RUN npm install -g slimerjs@1.0.0
