FROM node:8-alpine
LABEL author="Matheus Marchini <matheus@sthima.com>"
ENV NODE_ENV=production
COPY . /var/client-parser
WORKDIR /var/client-parser
RUN set -ex && \
    NODE_ENV="" npm install && \
    mv node_modules ..
CMD [ "node", "index.js" ]
