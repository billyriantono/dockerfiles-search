## Dockerfile
## https://docker.github.io/engine/reference/builder/
ARG base_img=3.10
FROM alpine:${base_img} AS production

## Legacy variant (alpine < 3.3)
#RUN set -ex; apk update && apk add wget && rm -rf /var/cache/apk/*
RUN set -ex; \
    apk add --no-cache \
    ca-certificates \
    python3 \
    uwsgi uwsgi-python3 

## Create system user and group
ONBUILD ARG user=worker
ONBUILD ENV USER=${user:-worker}
## BusyBox
ONBUILD RUN set -ex; addgroup -S ${user} && adduser -S -G ${user} ${user}
## Debian
#RUN set -ex; groupadd --system ${user} && useradd --system --gid ${user} ${user}

ADD src/test_container.sh /usr/bin/test_container.sh

EXPOSE 8080
WORKDIR /opt
CMD []
ENTRYPOINT ["/opt/entrypoint.sh"]
