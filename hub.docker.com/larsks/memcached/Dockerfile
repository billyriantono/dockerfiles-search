FROM alpine

RUN apk update; \
	apk add memcached

ENTRYPOINT ["/usr/bin/memcached", "-v", "-u", "memcached"]
