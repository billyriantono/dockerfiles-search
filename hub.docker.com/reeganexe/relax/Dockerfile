FROM alpine:3.8

RUN wget -qO- https://github.com/zerobotlabs/relax/releases/download/0.4.0/relax-stable-linux-amd64.1.tgz | \
  tar xzv -C /usr/local/bin && \
  apk add ca-certificates && \
  update-ca-certificates 2>/dev/null && \
  rm -rf /var/cache/apk/*

ENTRYPOINT ["relax"]
