FROM node:9-alpine
LABEL maintainer="Lyndon"
# Installs latest Chromium (68) package.
RUN apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/main "freetype>2.8" "harfbuzz>1.6" && \
    apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community udev ttf-freefont chromium nss && \
    apk add --no-cache make git curl && \
    mkdir -p /app && \
    mkdir -p /build

# Tell Puppeteer to skip installing Chrome. We'll be using the installed package.
ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD true