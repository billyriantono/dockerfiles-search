## Supports x86_64, x86, armhf, arm64, ppc64le
FROM amd64/debian:stretch as builder
RUN apt-get update && apt-get install -y curl gnupg
RUN ( \
    apt-key adv --batch --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-keys 0x1657198823e52a61 || \
    apt-key adv --batch --keyserver hkp://pgp.mit.edu:80 --recv-keys 0x1657198823e52a61 || \
    apt-key adv --batch --keyserver hkp://keyserver.pgp.com:80 --recv-keys 0x1657198823e52a61 || \
    apt-key adv --batch --keyserver hkp://ipv4.pool.sks-keyservers.net --recv-keys 0x1657198823e52a61 \
    ) && \
    echo "deb http://download.zerotier.com/debian/stretch stretch main" > /etc/apt/sources.list.d/zerotier.list
RUN apt-get update && apt-get install -y zerotier-one=1.4.2

FROM amd64/alpine:latest
LABEL version=1.4.2 \
    description="Containerized ZeroTier One for use on CoreOS or other Docker-only Linux hosts." \
    org.label-schema.schema-version="1.0" \
    org.label-schema.name="zerotier" \
    org.label-schema.description="Containerized ZeroTier One for use on CoreOS or other Docker-only Linux hosts." \
    org.label-schema.url="https://zerotier.com" \
    org.label-schema.version="1.4.2" \
    org.label-schema.docker.cmd="docker run --device=/dev/net/tun \
    --net=host \
    --cap-add=NET_ADMIN \
    --cap-add=SYS_ADMIN \
    -v /var/lib/zerotier-one:/var/lib/zerotier-one \
    -n zerotier-one \
    -d adb76/zerotier"

RUN apk add --no-cache libgcc libstdc++

RUN mkdir -p /var/lib/zerotier-one

COPY --from=builder \
    /var/lib/zerotier-one/zerotier-cli \
    /var/lib/zerotier-one/zerotier-idtool \
    /usr/sbin/zerotier-one \
    /usr/sbin/

CMD ["/usr/sbin/zerotier-one"]
