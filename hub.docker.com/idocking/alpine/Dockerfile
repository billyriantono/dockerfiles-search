FROM alpine:3.6

COPY entrypoint /

RUN set -eux; \
	apk add --no-cache --update tzdata ca-certificates coreutils su-exec>=0.2; \
	chmod +x /entrypoint

ENTRYPOINT ["/entrypoint"]