FROM alpine

RUN apk add --no-cache \
      openssl \
      ca-certificates \
      opensmtpd \
    && rm -rf /var/cache/apk/* \
    && mkdir -p /var/spool/smtpd

COPY smtpd.conf /etc/smtpd/
COPY docker-entrypoint.sh /usr/local/bin/
WORKDIR /var/spool/smtpd
EXPOSE 25
CMD "docker-entrypoint.sh"
