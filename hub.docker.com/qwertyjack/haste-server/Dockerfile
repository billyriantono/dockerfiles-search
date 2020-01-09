FROM node:alpine

RUN apk add git \
 && git clone -b production --single-branch --depth 1 https://github.com/seejohnrun/haste-server.git /opt/haste \
 && sed -i 's/https:\/\/ajax.googleapis\.com.*jquery\.min\.js/jquery.min.js/g' /opt/haste/static/index.html \
 && wget https://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js -O /opt/haste/static/jquery.min.js \
 && cd /opt/haste && npm install

WORKDIR /opt/haste
COPY config.js /opt/haste/

EXPOSE 7777
CMD ["npm", "start"]
