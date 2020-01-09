FROM alpine:latest
RUN apk --no-cache add dnsmasq
VOLUME ["/config"]
EXPOSE 53 53/udp
ENTRYPOINT ["dnsmasq", "-k", "--no-hosts", "--addn-hosts=/config/hosts", "--conf-file=/config/dnsmasq.conf"]
