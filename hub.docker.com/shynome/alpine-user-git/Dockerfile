FROM alpine
RUN set -xe && \
  apk add --no-cache openssh git nodejs && \
  adduser -s /bin/sh -h /root -D git
USER git
