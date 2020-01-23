FROM breauxaj/alpine:latest

RUN apk add haproxy \
  && rm -rf /var/cache/apk/*

COPY entrypoint.sh /entrypoint.sh

CMD ["/entrypoint.sh"]

EXPOSE 80

LABEL org.opencontainers.image.vendor="Breaux Heavy Industries" \
	org.opencontainers.image.url="https://breaux.io" \
	org.opencontainers.image.title="HAProxy Load Balancer" \
	org.opencontainers.image.description="HAProxy is a high performance load balancer for TCP and HTTP" \
	org.opencontainers.image.version="v0.0.1" \
	org.opencontainers.image.documentation="https://docs.breaux.io"