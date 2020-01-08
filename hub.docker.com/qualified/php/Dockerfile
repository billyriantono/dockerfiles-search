FROM composer:1.8 AS builder

COPY rootfs/workspace/project/composer.json /app/composer.json
RUN mkdir -p /app/src && composer install


FROM php:7.3.0-alpine

RUN set -ex; \
    adduser -D codewarrior; \
    ln -s /home/codewarrior /workspace;

COPY --from=builder --chown=codewarrior:codewarrior /app /workspace/project
COPY --chown=codewarrior:codewarrior rootfs/workspace/project /workspace/project

USER codewarrior
ENV USER=codewarrior \
    HOME=/home/codewarrior

COPY rootfs/opt/runner /opt/runner
WORKDIR /workspace/project
