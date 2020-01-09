FROM alpine:3.6

RUN apk --no-cache add openldap=2.4.44-r5 openldap-clients=2.4.44-r5

VOLUME /var/lib/openldap/openldap-data
VOLUME /etc/openldap/conf.d

EXPOSE 389 636

CMD ["slapd", "-d", "32768"]