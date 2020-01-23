FROM node:10

RUN curl -o- -L https://yarnpkg.com/install.sh | bash

WORKDIR /home/node/html
COPY package.json package.json
COPY yarn.lock yarn.lock
RUN yarn --pure-lockfile
COPY . .

RUN yarn link