FROM node:lts-alpine

ENV NODE_ENV=development \
    SERVER_PORT=8080

EXPOSE 8080

RUN apk add curl nano libsass --update-cache; \
    mkdir -p /app

COPY . /app

WORKDIR /app

RUN npm i npm -g; \
    npm install; \
    npm run build;

USER node

CMD ["node","/app/src/server/index.js"]