FROM alpine:latest

RUN apk add --update --wait 900 --progress mosquitto c-ares \
    && rm -rf /var/cache/apk/*
ADD config /mqtt/config
ADD entrypoint.sh /entrypoint.sh
RUN mkdir -p /mqtt/log \
    && chown -R mosquitto /mqtt \
    && chmod +x /entrypoint.sh

VOLUME ["/mqtt/data", "/mqtt/log"]
EXPOSE 1883 8883
ENTRYPOINT ["/entrypoint.sh"]