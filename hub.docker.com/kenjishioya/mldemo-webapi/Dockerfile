FROM node:10-alpine

RUN apk add --update tini \
    && mkdir -p /usr/src/app

EXPOSE 3000

WORKDIR /usr/src/app

COPY package.json .

RUN npm install && npm cache clean --force

COPY . .

CMD ["tini", "--", "npm", "run", "start"]