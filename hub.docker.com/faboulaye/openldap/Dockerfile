FROM debian:8
MAINTAINER Firdaws Aboulaye <aboufred@gmail.com>

ENV OPENLDAP_VERSION= \
 LDAP_PASSWORD=s3cr3tpassw0rd \
 DC1=example \
 DC2=org \
 LDAP_DOMAIN=$DC1.$DC2 \
 LDAP_ORGANISATION=$DC1-$DC2 \
 MAX_NOFILE=8192 \
 LDAP_HOME=/var/lib/ldap

COPY docker-entrypoint.sh /

RUN groupadd --gid 1000 -r openldap \
  && useradd -r --uid 1000 -c "OpenLDAP Server Account" -d $LDAP_HOME -g openldap -s /bin/false openldap \
  && apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install \
    --no-install-recommends -y slapd=${OPENLDAP_VERSION:-*} ldap-utils \
  && chmod +x /docker-entrypoint.sh \
  && chown openldap:openldap $LDAP_HOME /etc/ldap \
  && apt-get clean \
  && rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/*

VOLUME ["/etc/ldap", $LDAP_HOME]
EXPOSE 389

ENTRYPOINT ["/docker-entrypoint.sh"]
