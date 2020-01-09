FROM alpine:edge
MAINTAINER alex88, https://github.com/alex88/mosquitto-alpine-docker

RUN apk add --update mosquitto mosquitto-clients && mkdir /app && chown nobody /app 

VOLUME ["/app"]
WORKDIR /app

USER nobody

EXPOSE 1883

ENTRYPOINT ["mosquitto"]
