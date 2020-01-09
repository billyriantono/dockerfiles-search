FROM alpine:latest

RUN apk --no-cache add dnsmasq bind-tools

COPY docker-entrypoint.sh /docker-entrypoint.sh

EXPOSE 53 53/udp

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["dnsmasq"]