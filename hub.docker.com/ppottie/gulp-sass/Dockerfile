FROM node:alpine

LABEL maintenainer="Pierre Pottié <pierre.pottie@gmail.com>"

ENV NODEJS_UID 1000
ENV NODEJS_GID 1000


RUN \
  apk add --no-cache dumb-init && \
  npm update && \
  npm install --global gulp-cli && \
  npm install node-sass gulp gulp-sass && \
  chown -R node:node /srv && \
  npm rebuild node-sass

WORKDIR  /srv
VOLUME /srv

CMD ["gulp","watch"]