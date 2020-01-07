FROM alpine:latest

RUN apk update && apk upgrade \
  && rm -rf /var/cache/apk/*

CMD ["sh"]

LABEL org.opencontainers.image.vendor="Breaux Heavy Industries" \
	org.opencontainers.image.url="https://breaux.io" \
	org.opencontainers.image.title="Alpine Linux" \
	org.opencontainers.image.description="A base image utilized by child containers" \
	org.opencontainers.image.version="v0.0.1" \
	org.opencontainers.image.documentation="https://docs.breaux.io"