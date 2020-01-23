FROM node:10-alpine

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

ENV BUILD_DEPS='g++ gcc git make python' \
    LCB_PLUGINS='lets-chat-ldap lets-chat-s3'

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

ADD . .

RUN set -x \
&&  apk add --no-cache $BUILD_DEPS \
&&  npm install --production \
&&  npm install $LCB_PLUGINS \
&&  npm dedupe \
&&  rm -rf /tmp/npm* \
&&  apk del $BUILD_DEPS


RUN chown node:node uploads \
&&  mkdir -p builtAssets \
&&  chown node:node builtAssets

ENV LCB_DATABASE_URI=mongodb://mongo/letschat \
    LCB_HTTP_HOST=0.0.0.0 \
    LCB_HTTP_PORT=8080 \
    LCB_XMPP_ENABLE=true \
    LCB_XMPP_PORT=5222

USER node

EXPOSE 8080 5222

VOLUME ["/usr/src/app/config"]
VOLUME ["/usr/src/app/uploads"]

CMD ["npm", "start"]
