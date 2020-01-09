FROM alpine:3.7

ADD https://github.com/multiarch/qemu-user-static/releases/download/v2.11.1/qemu-arm-static /usr/bin/

ADD cross-build-start /usr/bin/
ADD cross-build-end /usr/bin/

RUN chmod +x /usr/bin/*

LABEL maintainer="drzef85@gmail.com"

ENTRYPOINT ["/bin/sh"]