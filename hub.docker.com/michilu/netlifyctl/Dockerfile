FROM alpine:edge

ARG version="0.4.0"

RUN apk --no-cache --update add \
  bash \
  ca-certificates \
  ;
RUN virtual=del \
  ; apk --no-cache --update add --virtual=${virtual} \
  curl \
  tar \
  && curl -sLf https://github.com/netlify/netlifyctl/releases/download/v${version}/netlifyctl-linux-amd64-${version}.tar.gz \
  | tar xzfp - -C /usr/local/bin \
  && apk del ${virtual}

ENTRYPOINT ["netlifyctl"]

WORKDIR /root
