FROM ubuntu:latest

RUN export DEBIAN_FRONTEND="noninteractive" && apt-get update \
    && apt-get install -y --allow-unauthenticated \
        language-pack-ru \
        sudo supervisor net-tools zenity \
        xvfb x11vnc \
        chromium-browser \
    && apt-get install -y lxqt openbox \        
    && apt-get autoclean \
    && apt-get autoremove \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get update
  
RUN update-locale LANG=ru_RU.UTF-8
RUN update-alternatives --display x-window-manager

ARG TINI_VERSION=v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /bin/tini
RUN chmod +x /bin/tini

COPY startup.sh /startup.sh
COPY conf /etc/supervisor/conf.d/supervisord.conf
RUN chmod +x startup.sh

EXPOSE 5900

WORKDIR /root

ENV VNC_PASSWORD=vnc_pass \
    USER=ubuntu \
    PASSWORD=ubuntu \
    SHELL=/bin/bash

ENTRYPOINT ["/startup.sh"]
