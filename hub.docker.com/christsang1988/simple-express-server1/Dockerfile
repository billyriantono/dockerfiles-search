FROM node:9.2.0

COPY index.js package.json /app/

WORKDIR /app

RUN yarn install && yarn cache clean --force

CMD node index.js
