FROM golang:alpine

LABEL maintainer "brad@bjc.id.au"

RUN apk update \
    && apk add --no-cache \
        su-exec \
        git \
        wget \
        openssl \
        ca-certificates \
    && update-ca-certificates \
    && wget -O- https://glide.sh/get | sh \
    && mv /go/bin/glide /usr/local/bin/glide

COPY entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]