FROM node:6.10.3-alpine
MAINTAINER Pankaj Tamrakar
#pankajpippin/dockerbase

RUN apk --update add curl ca-certificates openrc nginx 

#RUN npm install angular-cli -g 

 
# Create app directory
RUN mkdir -p /usr/src/app

RUN mkdir -p /etc/nginx/conf.d /tmp/nginx /var/log/nginx

WORKDIR /usr/src/app

RUN npm install -g  @angular/cli@latest