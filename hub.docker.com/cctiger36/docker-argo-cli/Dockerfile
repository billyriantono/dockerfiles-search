FROM alpine:3.10

RUN apk add --no-cache -t .build-deps curl \
 && rm -rf /var/cache/apk/* \
 && curl -sSL -o /usr/local/bin/argo https://github.com/argoproj/argo/releases/download/v2.4.2/argo-linux-amd64 \
 && chmod +x /usr/local/bin/argo

CMD ["argo"]
