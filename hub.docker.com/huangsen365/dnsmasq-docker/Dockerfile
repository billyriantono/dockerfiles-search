FROM alpine
RUN apk --no-cache add dnsmasq

COPY ./test.conf /etc/dnsmasq.d/

EXPOSE 53 53/udp
ENTRYPOINT ["dnsmasq", "-k"]
