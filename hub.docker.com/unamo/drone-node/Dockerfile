FROM node:10-alpine

LABEL maintainer="Adrian Dulić <adulic@gmail.com>"

RUN apk update && apk --no-cache add git rsync openssh

RUN addgroup -g 1001 drone && \
    adduser -D -u 1001 -G drone drone

CMD ["/bin/sh"]
