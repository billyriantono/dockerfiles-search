FROM alpine:3.7
MAINTAINER Kazumichi Yamamoto <yamamoto.febc@gmail.com>
LABEL MAINTAINER 'Kazumichi Yamamoto <yamamoto.febc@gmail.com>'

LABEL io.whalebrew.config.environment '["SAKURACLOUD_ACCESS_TOKEN", "SAKURACLOUD_ACCESS_TOKEN_SECRET" , "SAKURACLOUD_TRACE_MODE"]'

RUN set -x && apk add --no-cache --update zip ca-certificates

ADD https://github.com/sacloud/hanami/releases/download/v0.0.0/hanami_linux-amd64.zip ./
RUN unzip hanami_linux-amd64.zip -d /bin; rm -f hanami_linux-amd64.zip

VOLUME ["/workdir"]
WORKDIR /workdir

ENTRYPOINT ["/bin/hanami"]
CMD ["--help"]
