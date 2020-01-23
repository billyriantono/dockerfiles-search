FROM node:carbon

WORKDIR /coreone

COPY package*.json ./

RUN npm i
RUN npm i nodemon -g

COPY . .

EXPOSE 8080

CMD ["nodemon", "src/bin/server.js"]