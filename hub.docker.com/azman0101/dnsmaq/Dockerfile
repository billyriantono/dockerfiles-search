FROM i386/alpine:3.7  as build-env

RUN apk add --no-cache wget xz make g++ linux-headers nettle-dev

RUN wget http://www.thekelleys.org.uk/dnsmasq/dnsmasq-2.79.tar.xz

RUN tar xvf dnsmasq-2.79.tar.xz

RUN cd dnsmasq-2.79/ && make install \
   CFLAGS="-Wall -W -Os -fno-omit-frame-pointer" \
   COPTS="-DNO_DHCP -DNO_DHCP6 -DNO_SCRIPT -DNO_TFTP" \
   LDFLAGS=-static
RUN chmod +x dnsmasq-2.79/src/dnsmasq

FROM i386/alpine:3.7
RUN addgroup -S dnsmasq 2>/dev/null
RUN adduser -S -D -H -h /dev/null -s /sbin/nologin -G dnsmasq -g dnsmasq dnsmasq 2>/dev/null
COPY --from=build-env /dnsmasq-2.79/src/dnsmasq /
ENTRYPOINT [ "/dnsmasq" ]
