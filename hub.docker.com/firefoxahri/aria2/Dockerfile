FROM alpine:edge

ADD entrypoint.sh /entrypoint.sh

RUN apk update && \
	apk add --no-cache --update aria2

ENTRYPOINT ["/entrypoint.sh"]