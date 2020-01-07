FROM alpine:latest
MAINTAINER Chance Hudson

EXPOSE 443

COPY ./src /src
COPY ./bootstrap.sh /bootstrap.sh

RUN apk --no-cache add openvpn nodejs-npm python py-pip && \
  pip --no-cache-dir install awscli && \
  chmod +x /src/auth.js && \
  chmod +x /bootstrap.sh

WORKDIR /src

RUN rm -rf node_modules && \
  apk add --no-cache --virtual .build-deps g++ make python git && \
  npm install && \
  apk del .build-deps

COPY ./server.conf /etc/openvpn/server.conf

WORKDIR /etc/openvpn

ENTRYPOINT ["/bootstrap.sh"]
