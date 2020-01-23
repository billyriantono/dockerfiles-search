FROM node:8.9-slim

# crafted and tuned by pierre@ozoux.net and sing.li@rocket.chat
MAINTAINER cmk0923@hanmail.net

RUN groupadd -r rocketchat \
&&  useradd -r -g rocketchat rocketchat \
&&  mkdir -p /app \
&&  mkdir -p /app/uploads \
&&  chown rocketchat.rocketchat /app/uploads

VOLUME /app/uploads

# gpg: key 4FD08014: public key "Rocket.Chat Buildmaster <buildmaster@rocket.chat>" imported
RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys 0E163286C20D07B9787EBE9FD7F9D0414FD08104

ENV RC_VERSION 0.65.1

WORKDIR /app

RUN curl -fSL "https://releases.rocket.chat/${RC_VERSION}/download" -o rocket.chat.tgz \
&&  curl -fSL "https://releases.rocket.chat/${RC_VERSION}/asc" -o rocket.chat.tgz.asc \
&&  gpg --batch --verify rocket.chat.tgz.asc rocket.chat.tgz \
&&  tar zxvf rocket.chat.tgz \
&&  rm rocket.chat.tgz rocket.chat.tgz.asc \
&&  cd bundle/programs/server \
&&  npm install

RUN cd / \
&&  cd app

ADD . /app

# file modify
RUN cd / \
&&  rm -f bundle/programs/web.browser/111f6dfe3c5b59829f51d2620e189034953def3e.js \
&&  mv app/111f6dfe3c5b59829f51d2620e189034953def3e.js app/bundle/programs/web.browser/111f6dfe3c5b59829f51d2620e189034953def3e.js \
&&  rm -f bundle/programs/server/packages/rocketchat_channel-settings.js \
&&  mv app/rocketchat_channel-settings.js app/bundle/programs/server/packages/rocketchat_channel-settings.js \
&&  rm -f bundle/programs/server/packages/rocketchat_message-pin.js \
&&  mv app/rocketchat_message-pin.js app/bundle/programs/server/packages/rocketchat_message-pin.js

USER rocketchat

WORKDIR /app/bundle

# needs a mongoinstance - defaults to container linking with alias 'db'
ENV DEPLOY_METHOD=docker-official \
    MONGO_URL=mongodb://db:27017/lowpbrchat \
    HOME=/tmp \
    PORT=3000:3000 \
    ROOT_URL=http://localhost:3000 \
    Accounts_AvatarStorePath=/app/uploads

EXPOSE 3000

CMD ["node", "main.js"]