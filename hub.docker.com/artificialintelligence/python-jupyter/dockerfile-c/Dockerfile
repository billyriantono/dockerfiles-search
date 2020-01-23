FROM alpine
LABEL maintainer="LiveEdu <artem.merkulov@gmail.com>"

RUN apk add --no-cache rsyslog
COPY ./rsyslogd.conf /etc/rsyslogd.conf

ENTRYPOINT ["rsyslogd", "-n", "-f", "/etc/rsyslogd.conf"]

