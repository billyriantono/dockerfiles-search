FROM miktex/miktex

USER root

RUN apt-get update && \
    apt-get -y install ghostscript git curl

RUN rm -rf /var/lib/apt/lists/*

USER miktex
