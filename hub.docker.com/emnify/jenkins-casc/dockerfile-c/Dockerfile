FROM alpine:edge

RUN apk add \
    --update \
    --no-cache \
    curl \
    openssh \
    git \
    jq \
    py-pygments \
    && rm -rf /var/cache/apk/* \
    && curl -s https://kubernetes-helm.storage.googleapis.com/helm-v2.8.2-linux-amd64.tar.gz | tar xvzf - -C /usr/local/bin/ --strip-components 1 linux-amd64/helm

CMD ["helm"]

