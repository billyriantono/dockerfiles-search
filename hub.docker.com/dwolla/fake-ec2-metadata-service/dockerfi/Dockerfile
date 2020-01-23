FROM golang:1.10.1-alpine

ARG GLIDE_VERSION=v0.13.1

RUN apk add --update git && \
  rm -rf /var/cache/apk/*

RUN wget https://github.com/Masterminds/glide/releases/download/${GLIDE_VERSION}/glide-${GLIDE_VERSION}-linux-amd64.tar.gz && \
  tar xzf glide-${GLIDE_VERSION}-linux-amd64.tar.gz --strip-components=1 -C /usr/local/bin/ && \
  rm -f *.tar.gz

CMD ["/usr/local/bin/glide", "--version"]