FROM alpine:latest
MAINTAINER Lars Olzem <hackebein@gmail.com>
COPY compare.sh /entrypoint
RUN apk add --update --no-cache \
		bash \
		docker-cli \
		jq \
 && apk upgrade --update --no-cache \
 && wget https://storage.googleapis.com/container-diff/latest/container-diff-linux-amd64 -O /usr/local/bin/container-diff \
 && chmod +x /usr/local/bin/container-diff \
 && chmod +x /entrypoint
ENTRYPOINT ["/entrypoint"]
