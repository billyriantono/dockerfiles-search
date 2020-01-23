FROM node:8

WORKDIR /usr/src/app

COPY . .

RUN ls -all && npm install && npm install -g nodemon

CMD [ "npm", "start" ]