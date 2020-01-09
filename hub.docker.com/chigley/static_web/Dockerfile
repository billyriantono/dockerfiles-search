# Version: 0.0.1
FROM ubuntu:16.04
MAINTAINER Dean Logan Wood "dean@loganwood.co.uk"
ENTRYPOINT ["/usr/sbin/nginx"]
RUN apt-get update 
RUN apt-get install -y nginx
RUN echo 'Hi, I am in your container' \
    > /var/www/html/index.html
EXPOSE 80
