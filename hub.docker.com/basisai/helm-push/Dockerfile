ARG HELM_VERSION=2.14.3

FROM alpine/helm:${HELM_VERSION}

RUN apk add --update --no-cache git libressl ca-certificates \
    && helm init --client-only \
    && helm plugin install https://github.com/chartmuseum/helm-push \
    && apk del git \
    && rm -f /var/cache/apk/*
