FROM alpine:latest
RUN apk --no-cache --update add openvpn
EXPOSE 1194/udp
VOLUME /srv
ENTRYPOINT ["/usr/sbin/openvpn"]
