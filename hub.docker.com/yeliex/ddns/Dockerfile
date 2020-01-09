FROM node:alpine

RUN mkdir /ddns

WORKDIR /ddns

COPY ./ ./

RUN yarn && \
    npm run build && \
    rm -rf src/ node_modules/ tsconfig.json && \
    yarn --prod && \
    yarn cache clean

CMD node index.js
