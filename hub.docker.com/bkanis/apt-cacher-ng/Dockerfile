FROM alpine AS builder

# Download QEMU, see https://github.com/docker/hub-feedback/issues/1261
ENV QEMU_URL https://github.com/balena-io/qemu/releases/download/v3.0.0%2Bresin/qemu-3.0.0+resin-aarch64.tar.gz
RUN apk add curl && curl -L ${QEMU_URL} | tar zxvf - -C . --strip-components 1

FROM arm64v8/debian:stable-slim

# Add QEMU
COPY --from=builder qemu-aarch64-static /usr/bin

RUN apt-get update && apt-get install -y \
	apt-cacher-ng \
	&& rm -rf /var/lib/apt/lists/*

RUN echo 'PassThroughPattern: .*' >> /etc/apt-cacher-ng/acng.conf

VOLUME      ["/var/cache/apt-cacher-ng"]
EXPOSE      3142
CMD     chmod 777 /var/cache/apt-cacher-ng && /etc/init.d/apt-cacher-ng start && tail -f /var/log/apt-cacher-ng/*