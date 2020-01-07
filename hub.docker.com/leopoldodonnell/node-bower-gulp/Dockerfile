FROM node:0.12.7-slim

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

RUN npm install -g gulp
RUN npm install -g bower
RUN echo '{ "allow_root": true, "interactive": false }' > ~/.bowerrc

CMD [ "npm", "start" ]