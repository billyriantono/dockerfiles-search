FROM phusion/baseimage:latest

RUN mkdir -p /var/script

RUN apt-get update && apt-get install -y nodejs
RUN ln -s /usr/bin/nodejs /usr/bin/node
RUN apt-get install -y npm

RUN npm i -g laravel-echo-server

WORKDIR /var/script

RUN usermod -u 1000 www-data

EXPOSE 6001/tcp

CMD ["node", "/var/script/server.js"]
