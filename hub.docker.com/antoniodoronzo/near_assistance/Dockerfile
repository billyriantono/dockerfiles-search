FROM node:8-alpine

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

copy . .

EXPOSE 3000 3001

CMD [ "node", "server" ]
