#################################################################
#
#                    ##        .
#              ## ## ##       ==
#           ## ## ## ##      ===
#       /""""""""""""""""\___/ ===
#  ~~~ {~~ ~~~~ ~~~ ~~~~ ~~ ~ /  ===- ~~~
#       \______ o          __/
#         \    \        __/
#          \____\______/
#
#################################################################

FROM alpine:3.3
MAINTAINER Bohdan Tkachenko <bohdan@doc.ai>

RUN apk add --update rsyslog rsyslog-tls && rm -rf /var/cache/apk/*

ADD run.sh /tmp/run.sh
RUN chmod +x /tmp/run.sh
ADD rsyslog.conf /etc/
ADD loggly.crt /etc/rsyslog.d/keys/ca.d/

EXPOSE 514
EXPOSE 514/udp

ENTRYPOINT ["/tmp/run.sh"]
