#
# Dockerfile for pptpd
#

FROM alpine:3.9

RUN apk add --no-cache iptables ppp pptpd

CMD set -xe \
    && pptpd \
    && syslogd -n -O /var/log/messages
