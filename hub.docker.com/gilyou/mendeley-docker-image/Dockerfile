FROM ubuntu:bionic
ENV DEBIAN_FRONTEND noninteractive
LABEL maintainer "Renwu Gao <gilyou.public@gmail.com>"

RUN apt-get update && apt-get install -y --no-install-recommends \
    wget python gconf2 desktop-file-utils

RUN wget --no-check-certificate https://desktop-download.mendeley.com/download/apt/pool/main/m/mendeleydesktop/mendeleydesktop_1.18-stable_amd64.deb \
    && dpkg -i mendeleydesktop_1.18-stable_amd64.deb \
    && rm -rf /var/lib/apt/lists/* \
    && rm mendeleydesktop_1.18-stable_amd64.deb
