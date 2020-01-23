FROM alpine:3.8 AS downloader
ADD https://bin.equinox.io/c/VdrWdbjqyF/cloudflared-stable-linux-amd64.tgz /
RUN tar xf /cloudflared-stable-linux-amd64.tgz

FROM debian:stable-slim
RUN apt-get update && apt-get install -y ca-certificates && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
ENV TUNNEL_ORIGIN_CERT=/cert
COPY --from=downloader /cloudflared /usr/bin/cloudflared
USER nobody
CMD ["/usr/bin/cloudflared"]
