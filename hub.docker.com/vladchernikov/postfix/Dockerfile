FROM alpine:edge

RUN  apk --no-cache add postfix supervisor rsyslog

RUN chown root /var/spool/postfix/ && \
    chown root /var/spool/postfix/pid/

COPY ./supervisord.conf /etc/supervisor/supervisord.conf
COPY ./kill_supervisor.py /kill_supervisor.py

EXPOSE 25

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
