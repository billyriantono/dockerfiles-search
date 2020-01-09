FROM alpine:3.6

MAINTAINER Adrian Stachurski

ENV RSYSLOG_VERSION=8.18.0

COPY container-files/ /tmp/

RUN apk add --no-cache rsyslog && \
    apk add --no-cache logrotate && \
    cp -rf /tmp/etc / && \
    cp -f /tmp/etc/rtm-frontend.conf /etc/logrotate.d && \
    cp -f /tmp/etc/rtm-backend.conf /etc/logrotate.d && \
    cp -f /tmp/etc/oms-backend.conf /etc/logrotate.d && \
    cp -f /tmp/etc/aof-backend.conf /etc/logrotate.d && \
    cp -f /tmp/etc/aof-frontend.conf /etc/logrotate.d && \        	
    rm -rf "/tmp/"*

EXPOSE 515 515/udp

ENTRYPOINT ["rsyslogd", "-n"]]