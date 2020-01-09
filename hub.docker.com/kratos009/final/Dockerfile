FROM node:carbon

WORKDIR /messenger-webhook

ADD . /messenger-webhook

RUN npm install apiai 
RUN npm install mongodb
RUN npm install express
RUN npm install request

ENV Name node-server

EXPOSE 3000

CMD ["node","index.js"]
