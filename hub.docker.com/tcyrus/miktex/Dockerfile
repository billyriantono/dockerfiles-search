FROM debian:stretch-slim

LABEL description="Dockerized MiKTeX, Debian Stretch Slim"

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update -q && \
    apt-get install -yq --no-install-recommends \
        apt-transport-https \
        ca-certificates \
        gnupg \
        dirmngr && \
    rm -rf /var/lib/apt/lists/*

RUN apt-key adv --no-tty --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys D6BC243565B2087BC3F897C9277A7293F59E4889 && \
    echo "deb http://miktex.org/download/debian stretch universe" | tee /etc/apt/sources.list.d/miktex.list

RUN apt-get update -q && \
    apt-get install -yq --no-install-recommends \
        miktex \
        perl && \
    rm -rf /var/lib/apt/lists/*

RUN miktexsetup --shared=yes finish

RUN initexmf --admin --set-config-value [MPM]AutoInstall=1 && \
    mpm --admin --update && \
    initexmf --admin --update-fndb && \
    initexmf --admin --dump

RUN useradd -md /miktex miktex
USER miktex

WORKDIR /miktex/work
