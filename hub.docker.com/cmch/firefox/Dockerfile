FROM debian:10-slim 

ARG DEBIAN_FRONTEND=noninteractive

RUN \
    apt update && apt install -yq  \
    firefox-esr \
    && apt clean
