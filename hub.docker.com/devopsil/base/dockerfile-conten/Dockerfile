FROM alpine:3.10.2@sha256:72c42ed48c3a2db31b7dafe17d275b634664a708d901ec9fd57b1529280f01fb

LABEL description="Under the surface of llsd.de"
LABEL maintainer="Yann Duval <me@yannduval.de>"

RUN apk update && apk upgrade

ENV HUGO_VERSION=0.58.3
ADD https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz /tmp
RUN tar -xf /tmp/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz -C /tmp \
    && mkdir -p /usr/local/sbin \
    && mv /tmp/hugo /usr/local/sbin/hugo \
    && rm -rf /tmp/hugo_${HUGO_VERSION}_linux_amd64 \
    && rm -rf /tmp/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz \
    && rm -rf /tmp/LICENSE.md \
    && rm -rf /tmp/README.md

RUN apk add --update git python py-pip libressl \
    && apk upgrade \
    && pip install awscli \
    && apk --purge -v del py-pip \ 
    && apk add --no-cache ca-certificates
