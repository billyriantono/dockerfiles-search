FROM subspacelabs/ubuntu:arm32v7

WORKDIR /code

COPY docker/build.sh /build.sh

ENV DEV=true

RUN ["/build.sh"]
