FROM alpine/helm:latest

MAINTAINER Yuyang Gong

RUN apk add --update --no-cache git && \
    helm plugin install https://github.com/chartmuseum/helm-push && \
    apk del git && \
    rm -f /var/cache/apk/*

WORKDIR /apps

ENTRYPOINT ["helm"]
CMD ["--help"]