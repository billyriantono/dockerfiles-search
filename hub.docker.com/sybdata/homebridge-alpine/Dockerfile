FROM oznu/s6-node

RUN apk add --no-cache git python make g++ libffi-dev openssl-dev avahi avahi-compat-libdns_sd avahi-dev openrc dbus mc nano htop \
  && yarn global add npm \
  && yarn global add node-gyp \
  && mkdir /homebridge \
  && mkdir -p /home/root/homebridge

ENV HOMEBRIDGE_VERSION 0.4.22
RUN yarn global add homebridge@$HOMEBRIDGE_VERSION \
  && yarn add homebridge-vera \
  && yarn add homebridge-server 
 
WORKDIR /homebridge
VOLUME /homebridge

ENV S6_KEEP_ENV=1

COPY root /
