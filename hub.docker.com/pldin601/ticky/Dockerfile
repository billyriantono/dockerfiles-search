FROM node:9

WORKDIR /app

COPY package.json ./
COPY package-lock.json ./

RUN npm i

COPY . ./

CMD npm start
