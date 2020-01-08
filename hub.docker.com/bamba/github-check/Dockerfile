FROM alpine:3.6

RUN apk update; apk add curl openssl

ADD entrypoint.sh /
ENTRYPOINT ["/entrypoint.sh"]
