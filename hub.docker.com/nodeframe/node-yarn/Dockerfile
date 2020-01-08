FROM node:6.11.1-alpine
RUN apk update \
  && apk add curl bash binutils tar python \
  && apk add --update alpine-sdk \
  && rm -rf /var/cache/apk/* \
  && /bin/bash \
  && touch ~/.bashrc \
  && curl -o- -L https://yarnpkg.com/install.sh | bash \
  && apk del curl tar binutils

RUN yarn global add node-gyp
