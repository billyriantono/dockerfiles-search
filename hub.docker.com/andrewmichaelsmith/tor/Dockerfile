FROM alpine:3.6
RUN \
	echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> \
		/etc/apk/repositories && \
	apk add --update tor && \
	rm -rf /var/cache/apk/*
#USER tor
ENTRYPOINT ["tor"]
