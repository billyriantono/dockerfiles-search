FROM node:10-alpine
WORKDIR /app

ENV NODE_ENV production

RUN apk add --no-cache su-exec

RUN chown node:node /app; \
    npm install ghost-cli -g; \
    su-exec node ghost install --db=sqlite3 --no-prompt --no-stack --no-setup

ADD config.json /app

RUN npm install ghost-storage-adapter-s3 --prefix current/content/adapters/storage/s3; \
    mv current/content/adapters/storage/s3/node_modules/ghost-storage-adapter-s3/* current/content/adapters/storage/s3/; \
    mv config.json config.$NODE_ENV.json

EXPOSE 2368
CMD ["node", "current/index.js"]
