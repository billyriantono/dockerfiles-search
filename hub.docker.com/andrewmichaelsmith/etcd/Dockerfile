FROM alpine:edge
RUN \
	echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> \
		/etc/apk/repositories && \
	apk add --update etcd && \
	rm -rf /var/cache/apk/*
CMD ["etcd"]
