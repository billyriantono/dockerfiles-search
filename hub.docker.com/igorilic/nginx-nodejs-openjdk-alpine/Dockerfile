FROM igorilic/nginx-nodejs-bash-alpine:node7x

RUN apk update && \
      apk add --no-cache \
      python \
      build-base \
      openjdk8-jre-base \
      udev \
      ttf-freefont \
      chromium-chromedriver \
      chromium

ENV CHROME_BIN /usr/bin/chromium-browser

