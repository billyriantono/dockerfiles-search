FROM alpine:latest
MAINTAINER trezamere

EXPOSE 9091 51413 51413/udp

RUN adduser -HDu 39672 -s /sbin/nologin -h /var/lib/transmission -g transmission transmission

ARG VERSION
ARG REPOSITORY

RUN if [ -z ${VERSION+x} ] || [ -z ${REPOSITORY} ]; then \
	apk add --no-cache \
	curl \
	jq \
	openssl \
	p7zip \
	rsync \
	tar \
	transmission-cli \
	transmission-daemon \
	unrar \
	unzip; \
    else \
	apk add --no-cache --repository ${REPOSITORY} \
	curl \
	jq \
	openssl \
	p7zip \
	rsync \
	tar \
	transmission-cli=${VERSION} \
	transmission-daemon=${VERSION} \
	unrar \
	unzip; \
    fi

RUN mkdir /config /downloads /watch; \
	chown transmission:transmission \
	/config /downloads /watch

VOLUME /config /downloads /watch

USER transmission:transmission

ENTRYPOINT ["transmission-daemon"]
CMD ["--foreground", "--config-dir", "/config", "--download-dir", "/downloads", "--watch-dir", "/watch", "--no-portmap"]
