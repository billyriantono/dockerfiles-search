FROM alpine:3.8

RUN apk add --no-cache ca-certificates

RUN apk add --no-cache --virtual .fetch-deps \
		curl \
		tar \
	\
	&& curl -sSL "https://caddyserver.com/download/linux/amd64?license=personal&telemetry=off" | tar --no-same-owner --directory=/usr/bin/ --extract --gunzip caddy \
	&& chmod 0755 /usr/bin/caddy \
	&& /usr/bin/caddy -version \
	&& apk del .fetch-deps

WORKDIR /srv

ENTRYPOINT ["/usr/bin/caddy"]
CMD ["--conf", "/srv/conf/Caddyfile", "--log", "stdout"]
