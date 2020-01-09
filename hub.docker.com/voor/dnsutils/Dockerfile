FROM debian:stretch-slim

RUN apt-get update && apt-get install -y \
    curl \
    dnsutils \
    --no-install-recommends \
    && apt-get purge --auto-remove -y  \
    && rm -rf /var/lib/apt/lists/*