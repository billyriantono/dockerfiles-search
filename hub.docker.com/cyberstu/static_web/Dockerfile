# Version: 0.0.1
FROM ubuntu:14.04
MAINTAINER Stuart Wilson "stuart@hmtt.co.uk"
RUN apt-get update
RUN apt-get install -y nginx
RUN echo 'Hi, I am in your computer' \
  >/usr/share/nginx/html/index.html
EXPOSE 80
