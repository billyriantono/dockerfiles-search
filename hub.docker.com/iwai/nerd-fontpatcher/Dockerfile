FROM ubuntu:16.04

LABEL maintainer "Yuji Iwai <iwai.ug@gmail.com>"

ENV NERDFONTS_VERSION=2.0.0 \
    LANG=C.UTF-8

COPY entrypoint.sh /srv

RUN  apt-get update -qq \
  && apt-get -qq install -y --no-install-recommends software-properties-common \
  && add-apt-repository ppa:fontforge/fontforge \
  && apt-get update -qq \
  && apt-get install -y --no-install-recommends fontforge curl python-pip \
  && rm -rf /var/lib/apt/lists/* \
  && pip -q install configparser \
  && curl -sSL https://github.com/ryanoasis/nerd-fonts/archive/v${NERDFONTS_VERSION}.tar.gz -o /srv/v${NERDFONTS_VERSION}.tar.gz \
  && tar zxf /srv/v${NERDFONTS_VERSION}.tar.gz -C /srv \
  && rm -rf /srv/v${NERDFONTS_VERSION}.tar.gz /srv/nerd-fonts-${NERDFONTS_VERSION}/patched-fonts \
  && apt remove -y curl python-pip \
  && mkdir /data

WORKDIR /data

VOLUME ["/data"]

ENTRYPOINT ["/srv/entrypoint.sh"]
