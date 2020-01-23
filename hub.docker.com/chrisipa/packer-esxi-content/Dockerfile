FROM alpine:3.2

MAINTAINER chrisdaish@gmail.com

COPY logstash-forwarder /usr/bin/logstash-forwarder

WORKDIR /var/cache/logstash-forwarder

ENTRYPOINT ["/usr/bin/logstash-forwarder"]
CMD ["-config=/etc/logstash-forwarder.conf"]
