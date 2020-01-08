FROM alpine:latest

# install prereqs
RUN apk add --no-cache openssh-client tar curl

# install Caddy with Google Cloud DNS
RUN curl --silent --show-error --fail --location -o- \
	--header "Accept: application/tar+gzip, application/x-gzip, application/octet-stream" \
	https://caddyserver.com/download/linux/amd64?plugins=tls.dns.googlecloud | \
	tar --no-same-owner -C /usr/bin -xz caddy && \
	chmod 755 /usr/bin/caddy && \
	/usr/bin/caddy -version

# setup
WORKDIR /
EXPOSE 80 443
ENV CADDYFILE=/Caddyfile
ENV CADDYPATH=/caddy
ENV WWWPATH=/www
VOLUME /caddy

# run
ADD run.sh /run.sh
ENTRYPOINT ["/run.sh"]
