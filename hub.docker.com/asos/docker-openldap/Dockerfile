FROM debian:jessie

MAINTAINER Christian Luginbühl <dinkel@pimprecords.com>

ENV OPENLDAP_VERSION 2.4.40
ENV DEBUG_LEVEL 32768

# Build-time metadata as defined at http://label-schema.org
ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="ASoS OpenLDAP Docker" \
      org.label-schema.description="A docker container for running OpenLDAP." \
      org.label-schema.url="e.g. http://www.asosgaming.com/" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/asosgaming/docker-openldap" \
      org.label-schema.vendor="ASoS Gaming Community" \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0"


RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
        slapd=${OPENLDAP_VERSION}* && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN mv /etc/ldap /etc/ldap.dist

COPY modules/ /etc/ldap.dist/modules

COPY entrypoint.sh /entrypoint.sh

EXPOSE 389

VOLUME ["/etc/ldap", "/var/lib/ldap"]

ENTRYPOINT ["/entrypoint.sh"]

CMD ["sh", "-c", "slapd -d ${DEBUG_LEVEL} -u openldap -g openldap"]
