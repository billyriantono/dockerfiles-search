FROM alpine:3.8

RUN apk add --no-cache --virtual .build-dependencies curl git
RUN apk add --no-cache ca-certificates

RUN curl -L http://storage.googleapis.com/kubernetes-helm/helm-v2.11.0-linux-amd64.tar.gz | tar zxv -C /tmp
RUN mv /tmp/linux-amd64/helm /bin/helm
RUN mkdir -p ~/.helm/plugins
RUN helm init --client-only
RUN helm plugin install https://github.com/chartmuseum/helm-push
RUN apk del .build-dependencies
