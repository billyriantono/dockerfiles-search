FROM alpine:3.5
RUN apk add --no-cache rsyslog \
                       rsyslog-hiredis
COPY . /
VOLUME /var/run/rsyslog/dev
VOLUME [ "/var/log", "/etc/rsyslog.d" ]
ENTRYPOINT ["rsyslogd", "-n", "-f", "/etc/rsyslogd.conf"]
