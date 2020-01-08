FROM alpine:latest

RUN apk add --update --no-cache openvpn dropbear-ssh

ENTRYPOINT /usr/sbin/openvpn --up /etc/openvpn/up.sh --down /etc/openvpn/down.sh --script-security 2 --daemon --config /client.ovpn && /bin/sh
