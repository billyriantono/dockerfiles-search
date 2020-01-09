# arwineap/bitly-oauth2_proxy
FROM golang:alpine

RUN set -x \
    && apk add --no-cache git \
    && go get github.com/bitly/oauth2_proxy

EXPOSE 4180

CMD oauth2_proxy -config=/etc/oauth.ini
