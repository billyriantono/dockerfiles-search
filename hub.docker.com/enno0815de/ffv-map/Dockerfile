FROM node:carbon

WORKDIR /usr/src/app

RUN npm i grunt-cli -g

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 8080

CMD [ "npm", "start" ]