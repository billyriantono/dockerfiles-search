FROM node:11-alpine

RUN apk add --no-cache bash git openssh

RUN npm install -g http-server

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build

EXPOSE 3001

CMD ["http-server", "dist", "-p3001"]
