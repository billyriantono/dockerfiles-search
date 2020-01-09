FROM node:4-onbuild

MAINTAINER "Jatin Aneja <jatin.aneja@globallogic.com>"

RUN mkdir -p /usr/src/app

WORKDIR /usr/src/app

COPY . /usr/src/app/

RUN npm cache clean

RUN npm install

RUN npm install -g gulp

RUN apt-get update

RUN apt-get -y install nginx

RUN ["gulp","--env","testing"]

RUN cp -r dist/. /usr/share/nginx/html

COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80

CMD /usr/sbin/nginx -g "daemon off;"