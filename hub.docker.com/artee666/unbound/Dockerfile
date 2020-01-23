FROM alpine:latest

RUN apk add --update --no-cache \
	curl \
	unbound \
	&& curl -o /etc/unbound/root.hints https://www.internic.net/domain/named.cache \
	&& chmod 775 /etc/unbound \
	&& adduser unbound tty

EXPOSE 53/udp 53/tcp

COPY ./rootfs /

RUN chmod +x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]
