FROM alpine:3.10.3

RUN apk --no-cache add gettext npm

RUN npm install --unsafe-perm -g po2json@0.4.5 stonejs-tools@1.0.8

WORKDIR /app
