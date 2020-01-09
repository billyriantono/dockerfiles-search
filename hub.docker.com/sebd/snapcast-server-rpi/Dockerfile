FROM arm32v6/alpine:3.9.3
LABEL maintainer "Sebastian Daehne <daehne@rshc.de>"

ADD qemu-arm-static /usr/bin
RUN apk update && apk upgrade && apk add --no-cache snapcast-server

USER snapcast
CMD ["/usr/bin/snapserver"]