FROM alpine

VOLUME  [ "/data" ]
RUN apk add --no-cache tcpdump coreutils

ENTRYPOINT /usr/sbin/tcpdump $PARAMETERS

