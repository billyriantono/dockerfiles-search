# Build RADIUS container with MySQL, Kerberos, and LDAP support

FROM alpine:3.10.0

RUN addgroup -S -g 95 radius && \
    adduser -h /var/log/radius -s /sbin/nologin -g radius -G radius -u 95 -D -S -H radius

RUN apk add --no-cache freeradius-eap freeradius-krb5 freeradius-mysql freeradius-ldap krb5

RUN touch /etc/keytab && chown root:radius /etc/keytab && chmod 640 /etc/keytab

#RUN rm -rf /etc/raddb && mkdir -p /etc/raddb && chown root:radius /etc/raddb && chmod 755 /etc/raddb
RUN mv /etc/raddb /etc/raddb.local && mkdir -p /etc/raddb && chown root:radius /etc/raddb && chmod 755 /etc/raddb

COPY krb5.conf /etc/

EXPOSE 1812 1813 1812/udp 1813/udp 18120/udp

USER radius

VOLUME /etc/raddb
VOLUME /var/log/radius

# for debugging, use
CMD [ "/usr/sbin/radiusd", "-X" ]
# and look at the journald log

#CMD [ "/usr/sbin/radiusd", "-f" ]
