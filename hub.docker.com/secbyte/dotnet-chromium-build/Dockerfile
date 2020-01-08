FROM secbyte/dotnet-build:latest

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        -y chromium-driver && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*
