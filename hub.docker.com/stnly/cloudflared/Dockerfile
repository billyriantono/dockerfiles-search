FROM debian:buster-slim

RUN apt-get update \
 && apt-get install -y curl \
 && curl https://bin.equinox.io/c/VdrWdbjqyF/cloudflared-stable-linux-amd64.tgz -o /cloudflared.tgz \
 && tar -xzvf /cloudflared.tgz

FROM alpine:latest

COPY --from=0 /cloudflared /usr/bin/cloudflared
RUN apk update \
 && apk add libc6-compat ca-certificates \
 && rm -rf /var/cache/apk/* \
 && chmod +x /usr/bin/cloudflared

ENTRYPOINT ["cloudflared"]

