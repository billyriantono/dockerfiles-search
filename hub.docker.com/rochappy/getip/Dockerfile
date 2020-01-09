FROM alpine:latest

RUN apk update \
    && apk add curl

ENTRYPOINT [ "curl", "-s", "https://ipinfo.io/" ]
