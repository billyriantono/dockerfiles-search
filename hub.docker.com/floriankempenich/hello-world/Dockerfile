FROM node:alpine

RUN mkdir /app
WORKDIR /app

ADD ./package.json .
RUN npm install 

ADD . .

CMD ["node", "app.js"]
