FROM alpine:3.3
RUN apk --update-cache add curl \
  && rm -rf /var/cache/apk/*

ENV CONFD_VERSION "0.11.0"
RUN curl -fsSL "https://github.com/kelseyhightower/confd/releases/download/v$CONFD_VERSION/confd-$CONFD_VERSION-linux-amd64" \
    -o /usr/bin/confd \
  && chmod u+x /usr/bin/confd
