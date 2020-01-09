FROM alpine:3.6

LABEL maintainer="We ahead <docker@weahead.se>"

ENV RANCHER_CLI_VERSION="0.6.3"

RUN apk --no-cache add --virtual build-deps curl \
  && curl -L "https://releases.rancher.com/cli/v${RANCHER_CLI_VERSION}/binaries/linux-amd64/rancher.xz" | xzcat - > /usr/local/bin/rancher \
  && chmod +x /usr/local/bin/rancher \
  && apk del build-deps \
  && apk --no-cache add openssl ca-certificates \
  && update-ca-certificates

WORKDIR /data

ENTRYPOINT [ "/usr/local/bin/rancher" ]
