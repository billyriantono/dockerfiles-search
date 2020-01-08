FROM debian:buster-slim

RUN apt update && \
    apt install --no-install-recommends --assume-yes curl && \
    rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["curl"]
