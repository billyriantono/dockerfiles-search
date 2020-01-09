FROM node:8

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

ENV DB_CONNECTION_STRING='mongodb://nodejs:1234@192.168.1.80:27017/phoenix'
ENV PORT=3000

CMD [ "npm", "start" ]
