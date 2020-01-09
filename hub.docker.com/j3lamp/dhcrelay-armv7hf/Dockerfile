FROM resin/armv7hf-alpine:3.8

RUN [ "cross-build-start" ]

RUN set -xe \
	&& apk add --update --no-cache dhcrelay tzdata \
	&& rm -rf /var/cache/apk/*


RUN [ "cross-build-end" ]

ADD entrypoint.sh /entrypoint.sh
ENTRYPOINT [ "/entrypoint.sh" ]
