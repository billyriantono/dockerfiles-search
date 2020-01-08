FROM node:7.4-alpine

MAINTAINER Kalle R. Møller <docker@k-moeller.dk>

RUN npm install -g http-server

VOLUME /var/www

ENTRYPOINT http-server

CMD /var/www

EXPOSE 8080
