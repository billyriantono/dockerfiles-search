FROM phusion/baseimage:latest

MAINTAINER Matt Alford <malford@nsgdv.com>

RUN mkdir -p /var/script

RUN apt-get update && apt-get install -y nodejs
RUN ln -s /usr/bin/nodejs /usr/bin/node
RUN apt-get install -y npm
RUN /usr/bin/npm install express && /usr/bin/npm install request 

# Upgrade node and npm to latest version
RUN     npm cache clean
RUN     npm install -g n
RUN     n stable
RUN     curl -L https://npmjs.org/install.sh | sh

WORKDIR /var/script

RUN usermod -u 1000 www-data

EXPOSE 3000/tcp

# CMD ["node", "/var/script/server.js"]
# CMD ["/var/script/server.sh"]
