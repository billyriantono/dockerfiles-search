FROM node:10-alpine

RUN npm install -g --unsafe-perm \
      homebridge \
      homebridge-nest \
      homebridge-hue \
      homebridge-webos-tv

RUN mkdir -p /root/.homebridge
VOLUME /root/.homebridge

ENTRYPOINT [ "homebridge" ]

