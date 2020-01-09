FROM node:8

WORKDIR /namesilo
VOLUME /config

ADD . .
RUN npm ci


CMD [ "npm", "start" ]
