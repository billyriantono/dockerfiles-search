FROM gliderlabs/alpine:3.3

RUN apk --no-cache add \
    nodejs \
    git

COPY ./start.sh /tmp
CMD sh /tmp/start.sh
