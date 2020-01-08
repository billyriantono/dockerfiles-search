FROM node:alpine

WORKDIR /usr/src/app

COPY package.json /usr/src/app/

RUN npm install

COPY app.js /usr/src/app/

ENV ENV prod

CMD [ "node" , "app.js" ]
