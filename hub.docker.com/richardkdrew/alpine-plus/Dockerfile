# DOCKER VERSION 1.12.0
#
# Alpine (with some basic tools) Dockerfile
#
# https://github.com/richardkdrew/dockerfiles
#
FROM alpine:3.4

RUN apk add --update \
        bash \
        nano \
        openssh \
        apache2-utils \
    && rm -rf /tmp/* /var/cache/apk/* /root/.cache/*

CMD ["/bin/bash"]