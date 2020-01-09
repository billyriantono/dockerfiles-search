FROM node:10-alpine

RUN apk update
RUN apk add curl bash gnupg

RUN touch $HOME/.profile

RUN curl -o- -L https://yarnpkg.com/install.sh | bash

RUN ln -s /root/.yarn/bin/yarn /usr/bin/yarn
