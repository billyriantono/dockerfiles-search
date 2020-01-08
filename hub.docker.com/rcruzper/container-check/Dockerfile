FROM alpine:3.5
MAINTAINER Raúl Cruz

RUN apk add --no-cache curl

ADD entrypoint.sh .

ENTRYPOINT ["./entrypoint.sh"]

