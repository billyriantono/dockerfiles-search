FROM ubuntu:19.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y \
      ca-certificates \
    && rm -rf /var/lib/apt/lists/*