FROM alpine:3.10.3

RUN apk --update add \
        postfix \
        rsyslog \
        supervisor \
    && rm -rf /var/cache/apk/*

COPY postfix/main.cf /etc/postfix/main.cf
COPY postfix/master.cf /etc/postfix/master.cf

COPY supervisor/supervisord.conf /etc/supervisord.conf
RUN mkdir -p /etc/supervisor.d
COPY supervisor/supervisor.d/*.ini /etc/supervisor.d/

COPY run.sh /run.sh
RUN chmod 755 /run.sh

ENTRYPOINT ["/run.sh"]
