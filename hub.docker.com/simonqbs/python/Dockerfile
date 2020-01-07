FROM python:2.7-slim

RUN apt-get update && apt-get install -y --no-install-recommends \
                ca-certificates \
                libsqlite3-0 \
                libssl1.0.0 \
                build-essential \
                git-core \
                curl \
                zlib1g-dev \
                libpcre3-dev \
                libc-ares-dev \
        && rm -rf /var/lib/apt/lists/*
