FROM ghost:2.7.1-alpine

RUN yarn add ghost-github-storage && mkdir -p current/core/server/adapters/storage && cp -vR node_modules/ghost-github-storage current/core/server/adapters/storage/ghost-github-storage 

EXPOSE 2368