FROM alpine
MAINTAINER OpenGG <liy099@gmail.com>

RUN apk update \
    && apk add --no-cache aria2

VOLUME /config /downloads

EXPOSE 6800

ENTRYPOINT ["aria2c"]
CMD ["--conf-path=/config/aria2.conf", ">", "/dev/stdout", "2", ">", "/dev/stderr"]
