# dnsmasq Dockerfile
# Alpine Linux Base OS
# Sets up DNSMASQ as a DNS server applying block rules to all 'bad' domains reported by SANS
# https://isc.sans.edu/suspicious_domains.html

FROM scratch
MAINTAINER github@thehurleys.net
ADD alpine-minirootfs-3.5.1-x86_64.tar.gz /

ARG APK_FLAGS_COMMON="-q"
#ARG APK_FLAGS_PERSISTENT="${APK_FLAGS_COMMON} --clean-protected --no-cache"
ARG APK_FLAGS_DEV="${APK_FLAGS_COMMON} --no-cache"

RUN apk update && \
	apk add ${APK_FLAGS_DEV} \
	bash \
	git \
	bind-tools \
	dnsmasq \
	wget && \
	rm -rf /var/cache/apk/*

COPY block /etc/dnsmasq.d/
COPY dnsmasq.conf /etc/

EXPOSE 53/TCP 53/UDP

ENTRYPOINT ["/usr/sbin/dnsmasq", "-k", "--user=root"]

