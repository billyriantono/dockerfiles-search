FROM alpine:3.6

LABEL maintainer="lukasz.gogolin@msales.com"

ADD https://s3.eu-central-1.amazonaws.com/msales-alpine-repo/nss_wrapper-1.1.3-r0.apk /tmp/

ENV ENV="/etc/profile"

RUN apk --update add ca-certificates curl \
    && apk add --allow-untrusted /tmp/nss_wrapper-1.1.3-r0.apk \
    && rm -rf /var/cache/apk/* \
    && rm -rf /tmp/*.apk \
    && mkdir -p /opt/app-root /opt/sys \
    && adduser -h /opt/app-root -u 1001 -H -D builder \
    && chown -R builder:root /opt/app-root /opt/sys \
	&& chmod -R g+w /opt/app-root /opt/sys

ADD files/entrypoint.sh /opt/sys/
ADD files/env.sh /etc/profile.d/

RUN chown -R builder:root /opt/app-root /opt/sys \
    && chmod -R g+w /opt/app-root /opt/sys

ENTRYPOINT [ "/opt/sys/entrypoint.sh" ]
