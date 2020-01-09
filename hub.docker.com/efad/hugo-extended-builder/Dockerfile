FROM alpine:3.8

LABEL maintainer="Balazs Nadasdi <yitsushi@protonmail.ch>"

ENV VERSION "0.52"

RUN apk add --no-cache curl git yarn py-pygments && \
      curl -sL https://github.com/gohugoio/hugo/releases/download/v${VERSION}/hugo_extended_${VERSION}_Linux-64bit.tar.gz \
            -o /tmp/hugo.tar.gz && \
      tar -xzf /tmp/hugo.tar.gz -C /tmp && \
      mv /tmp/hugo /usr/bin/hugo && \
      rm -rf /tmp/* && \
      apk del curl

CMD ["hugo"]
