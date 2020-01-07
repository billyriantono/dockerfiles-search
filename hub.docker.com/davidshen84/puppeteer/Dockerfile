FROM node:11-alpine
LABEL maintainer="Xi Shen <davidshen84@gmail>" \
  node=11 \
  alpine=true \
  chromium=edge

ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD=true

# Installs latest Chromium package.
RUN echo @edge http://nl.alpinelinux.org/alpine/edge/community >> /etc/apk/repositories && \
  echo @edge http://nl.alpinelinux.org/alpine/edge/main >> /etc/apk/repositories && \
  apk update && apk upgrade && \
  apk add --no-cache \
  chromium@edge \
  nss@edge

