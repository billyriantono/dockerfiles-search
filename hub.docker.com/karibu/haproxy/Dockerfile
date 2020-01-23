FROM haproxy:alpine

LABEL maintainer="paascencio@gmail.com"

RUN apk upgrade --update && \
    apk add rsyslog

COPY haproxy.cfg /etc/
COPY rsyslog.conf /etc/rsyslog.d/
COPY docker-entrypoint.sh /usr/bin/docker-entrypoint.sh

ENTRYPOINT [ "/usr/bin/docker-entrypoint.sh" ]

CMD ["haproxy","-f","/etc/haproxy.cfg"]
