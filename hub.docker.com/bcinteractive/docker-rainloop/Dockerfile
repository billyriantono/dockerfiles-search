FROM alpine:3.8 AS builder

ARG RAINLOOP_VERSION="1.12.1"
ARG GPG_FINGERPRINT="3B79 7ECE 694F 3B7B 70F3  11A4 ED7C 49D9 87DA 4591"

RUN apk add --update \
        wget \
        gnupg \
    && wget --quiet --output-document rainloop-v${RAINLOOP_VERSION}.zip https://github.com/RainLoop/rainloop-webmail/releases/download/v${RAINLOOP_VERSION}/rainloop-${RAINLOOP_VERSION}.zip \
    && wget --quiet --output-document rainloop-v${RAINLOOP_VERSION}.zip.asc https://github.com/RainLoop/rainloop-webmail/releases/download/v${RAINLOOP_VERSION}/rainloop-${RAINLOOP_VERSION}.zip.asc \
    && wget --quiet --output-document rainloop.asc http://www.rainloop.net/repository/RainLoop.asc \
    && gpg --import rainloop.asc \
    && FINGERPRINT=$(LANG=C gpg --verify rainloop-v${RAINLOOP_VERSION}.zip.asc rainloop-v${RAINLOOP_VERSION}.zip 2>&1 | sed -n "s/Primary key fingerprint: \(.*\)/\1/p") \
    && if [ -z "${FINGERPRINT}" ]; then echo "ERROR: Invalid GPG signature!"; exit 1; fi \
    && if [ "${FINGERPRINT}" != "${GPG_FINGERPRINT}" ]; then echo "ERROR: Invalid GPG fingerprint!"; exit 1; fi \
    && mkdir /rainloop \
    && unzip -q /rainloop-v${RAINLOOP_VERSION}.zip -d /rainloop \
    && find /rainloop -type d -exec chmod 755 '{}' \; \
    && find /rainloop -type f -exec chmod 644 '{}' \;


FROM php:7.2.12-fpm-alpine3.8
COPY --from=builder /rainloop /data
RUN chown -R www-data:www-data /data
