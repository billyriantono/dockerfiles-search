FROM node:10.14-alpine

# Installs latest Yarn package.
RUN apk update && apk upgrade \
    && rm -rf /var/lib/apt/lists/* \
    /var/cache/apk/* \
    /usr/share/man \
    /tmp/* \
    && npm install -g -s --no-progress yarn \
    && yarn cache clean \
    && npm cache clean --force