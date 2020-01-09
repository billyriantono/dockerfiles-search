FROM ubuntu:18.04

RUN apt-get update && apt-get install -y \
        build-essential \
        libssl-dev

RUN groupadd -r bootgen && useradd -g bootgen bootgen
COPY --chown=bootgen:bootgen / /usr/bootgen
WORKDIR /usr/bootgen

USER bootgen
RUN make
