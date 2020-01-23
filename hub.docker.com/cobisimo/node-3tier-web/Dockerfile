FROM node:10.4.1-alpine

WORKDIR /usr/app

COPY package.json .
RUN npm install --quiet

COPY . .

EXPOSE 8000

RUN npm install

CMD npm start
