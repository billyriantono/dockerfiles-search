FROM balenalib/raspberrypi3-alpine:3.11

LABEL version="4.9-armv7hf"
LABEL maintainer="Emanuel Freitas <emanuelfreitas@outlook.com>"

RUN [ "cross-build-start" ]

# http://alpine.gliderlabs.com/alpine/v3.11/main/armhf/
RUN apk add --no-cache squid=4.9-r0

COPY entrypoint.sh /sbin/entrypoint.sh

RUN chmod 755 /sbin/entrypoint.sh

RUN [ "cross-build-end" ]

EXPOSE 3128/tcp
ENTRYPOINT ["sh", "/sbin/entrypoint.sh"]