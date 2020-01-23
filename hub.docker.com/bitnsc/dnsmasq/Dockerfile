FROM alpine:3.3
RUN apk --no-cache add dnsmasq
EXPOSE 53 53/udp
ADD run.sh /
ENTRYPOINT ["/run.sh"]
