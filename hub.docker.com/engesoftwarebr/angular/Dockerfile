FROM alpine:latest
LABEL maintainer="ruy.silva@engesoftware.com"
WORKDIR /var/www

ENV CHROME_BIN="/usr/bin/chromium-browser"
ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD="true"

RUN apk add --update --upgrade git nodejs nodejs-npm chromium && npm i -g yarn @angular/cli@latest
