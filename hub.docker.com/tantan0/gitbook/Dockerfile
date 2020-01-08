FROM node:alpine

LABEL maintainer="tantan0"

RUN apk add --no-cache git curl fontconfig  \
  && curl -O https://noto-website-2.storage.googleapis.com/pkgs/NotoSansCJKjp-hinted.zip \
  && mkdir -p /usr/share/fonts/opentype/noto \
  && unzip NotoSansCJKjp-hinted.zip -d /usr/share/fonts/opentype/noto \
  && rm NotoSansCJKjp-hinted.zip \
  && fc-cache -fv \
  && apk del curl

RUN npm install -g gitbook-cli && gitbook fetch latest

EXPOSE 4000
WORKDIR /docs

CMD ["gitbook","--help"]
