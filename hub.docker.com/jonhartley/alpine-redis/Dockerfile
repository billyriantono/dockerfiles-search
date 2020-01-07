FROM alpine:3.8

RUN set -xe && apk add --update --no-cache redis bash

COPY entrypoint.sh /entrypoint.sh

EXPOSE 6379 16379

ENTRYPOINT ["/entrypoint.sh"]
