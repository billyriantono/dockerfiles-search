FROM alpine:3.10
MAINTAINER Simon Frankenberger <simon@fraho.eu>

ARG JAVA_PKG=openjdk11-jre
ARG KEYCLOAK_VERSON=6.0.1
ARG KEYCLOAK_SHA1=472b37ccc9b5bb3119295c2880db49aada2fe9ed
ARG KEYCLOAK_URL=https://downloads.jboss.org/keycloak/${KEYCLOAK_VERSON}/keycloak-${KEYCLOAK_VERSON}.tar.gz

RUN set -x \
	&& apk --no-cache upgrade \
	&& apk --no-cache add $JAVA_PKG wget tini \
	&& mkdir -p /opt/jboss \
	&& wget -O /opt/jboss/keycloak.tgz "$KEYCLOAK_URL" \
	&& cd /opt/jboss \
	&& echo "$KEYCLOAK_SHA1  keycloak.tgz" | sha1sum -c - \
	&& tar -xzf keycloak.tgz \
	&& mv keycloak-${KEYCLOAK_VERSON} keycloak \
	&& rm keycloak.tgz \
	&& apk --no-cache del wget \
	&& addgroup jboss \
	&& adduser -h /opt/jboss -s /bin/ash -G jboss -D jboss

USER jboss

CMD [ "/sbin/tini", "-g", "--", "/opt/jboss/keycloak/bin/standalone.sh" ]

EXPOSE 9990 8443

# vim: set ft=dockerfile:
