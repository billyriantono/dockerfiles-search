FROM ubuntu:latest

LABEL maintainer="sotif"

ENV NGINX_OBS_AUTOMATIC_LOW_BITRATE_SWITCHING_VERSION 1.2.4

# Install dependencies
RUN apt-get update && \
    apt-get install -y wget npm 

WORKDIR /usr/src/bitrate-switcher

RUN wget -O nginx-obs-automatic-low-bitrate-switcher-${NGINX_OBS_AUTOMATIC_LOW_BITRATE_SWITCHING_VERSION}.tar.gz https://github.com/sotif/nginx-obs-automatic-low-bitrate-switching/archive/v${NGINX_OBS_AUTOMATIC_LOW_BITRATE_SWITCHING_VERSION}.tar.gz && \
    tar -zxf nginx-obs-automatic-low-bitrate-switcher-${NGINX_OBS_AUTOMATIC_LOW_BITRATE_SWITCHING_VERSION}.tar.gz && \
    cd nginx-obs-automatic-low-bitrate-switching-${NGINX_OBS_AUTOMATIC_LOW_BITRATE_SWITCHING_VERSION} && \
    npm install --production

WORKDIR /usr/src/bitrate-switcher/nginx-obs-automatic-low-bitrate-switching-${NGINX_OBS_AUTOMATIC_LOW_BITRATE_SWITCHING_VERSION}


CMD ["npm", "start"]
