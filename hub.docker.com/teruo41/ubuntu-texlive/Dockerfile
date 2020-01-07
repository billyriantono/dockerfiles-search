FROM ubuntu:disco

ENV DEBIAN_FRONTEND=noninteractive

RUN set -x \
      && apt-get update \
      && apt-get -y install \
           texlive-full \
           make \
           imagemagick \
           inkscape \
           latexmk \
           git \
           openssh-client \
      && rm -rf /var/lib/apt/lists/* \
      && kanji-config-updmap-sys ipaex

