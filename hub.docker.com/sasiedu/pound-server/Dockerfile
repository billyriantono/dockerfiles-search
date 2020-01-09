FROM node:10.14.2-jessie

RUN mkdir -p /var/app/
WORKDIR /var/app

COPY . /var/app/

RUN yarn install

CMD [ "node", "server.js" ]