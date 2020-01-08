FROM node:10.16.0-alpine

ENV ALPINE_VERSION edge
ENV NODE_VERSION 10.16.0
ENV CHROMIUM_VERSION 73
ENV FREETYPE_VERSION 2.9.1-r2
ENV HARFBUZZ_VERSION 2.5.2-r0
ENV CHROME_BIN /usr/bin/chromium-browser

# Install Node & Chromium
RUN apk add --no-cache \
    chromium \
    freetype \
    harfbuzz \
    nss \
    git \
    bash \
    curl \
    && rm -rf /var/cache/* \
    && mkdir /var/cache/apk
