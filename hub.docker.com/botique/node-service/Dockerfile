FROM node:8.1.4

RUN apt-get update && apt-get install -y curl apt-transport-https && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y yarn

ENV NODE_ENV production

ONBUILD ADD ./package.json ./
ONBUILD ADD ./yarn.lock ./
ONBUILD RUN yarn --no-progress

CMD node bundle.js