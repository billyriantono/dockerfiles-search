FROM debian:buster-slim
LABEL maintainer="blue271828"
# If you set a Linux image, please check stable versions of TeX Live by
# https://packages.debian.org/search?keywords=texlive
# TeX Live packages don't always stable for Debian versions.

RUN apt-get update && apt-get install -y \
    texlive-full=2018.20190227-2 \
    && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
