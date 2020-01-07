FROM alpine:latest

MAINTAINER Josh Williams <th3prime@codingprime.com>

RUN apk --update add --no-cache \
		bash \
		dbus-x11 \
		mesa-gl \
		virt-manager

CMD ["/usr/bin/virt-manager", "--no-fork"]
