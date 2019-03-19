FROM node:8-alpine

ENV HUGO_VERSION 0.53
ENV HUGO_BINARY hugo_${HUGO_VERSION}_Linux-64bit.tar.gz

# Install Hugo
RUN set -x && \
  apk add --update wget ca-certificates && \
  wget https://github.com/spf13/hugo/releases/download/v${HUGO_VERSION}/${HUGO_BINARY} && \
  tar xzf ${HUGO_BINARY} && \
  rm -r ${HUGO_BINARY} && \
  mv hugo /usr/bin && \
  rm /var/cache/apk/*

COPY ./ /site

WORKDIR /site

RUN npm install -g gulp
RUN npm install
RUN npm run getembeds
RUN gulp sass && hugo

FROM nginx

COPY --from=0 /site/public /usr/share/nginx/html
