FROM node:7

RUN npm install -g bower node-sass coffee-script pug-cli uglify-js wiredep-cli bowcat nodemon

WORKDIR /srv/app

COPY ./scripts /opt/scripts

CMD /opt/scripts/watch
