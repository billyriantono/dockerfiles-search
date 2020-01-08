FROM golang:alpine AS builder

RUN apk add -U --no-cache -t .dep \
	gcc \
	git \
	libjpeg-turbo-dev \
	libwebp-dev \
	musl-dev \
    && go get -u manael.org/x/manael/cmd/manael \
    && cd /tmp \
	&& mkdir -p rootfs/usr/bin \
	&& cp /go/bin/manael rootfs/usr/bin \
	&& mkdir -p rootfs/lib rootfs/usr/lib \
	&& for lib in $(ldd rootfs/usr/bin/manael | awk '{ print $(NF-1) }'); do cp $lib rootfs$lib; done \
	&& mkdir -p rootfs/etc/ssl/certs \
	&& cp /etc/ssl/certs/ca-certificates.crt rootfs/etc/ssl/certs

FROM scratch

COPY --from=builder /tmp/rootfs /

CMD ["manael"]
