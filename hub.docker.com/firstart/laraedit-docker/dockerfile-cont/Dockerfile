FROM alpine:edge
RUN apk add --no-cache -X http://dl-cdn.alpinelinux.org/alpine/edge/testing amule && \
    addgroup -g 1001 -S amule && \
    adduser -G amule -u 1001 -S -s /sbin/nologin amule
EXPOSE 4713 6883 6893/udp
VOLUME /home/amule/.aMule /incoming
USER amule:amule
ENTRYPOINT ["amuled"]