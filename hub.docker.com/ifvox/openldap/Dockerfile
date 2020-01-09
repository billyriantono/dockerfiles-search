FROM alpine:3.5

COPY docker-entrypoint.sh /docker-entrypoint.sh

RUN \
  apk add --no-cache ldapvi openldap openldap-back-hdb openldap-back-bdb openldap-clients && \
  chown -R ldap /var/run/openldap && \
  ln -s /var/run/openldap /var/run/slapd

EXPOSE 389 636

ENTRYPOINT ["/docker-entrypoint.sh"]
