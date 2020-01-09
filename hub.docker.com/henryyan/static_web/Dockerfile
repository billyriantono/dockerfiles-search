# Version: 0.0.1
FROM ubuntu:18.04
MAINTAINER  Henry Yan "yanhonglei@gmail.com"
RUN apt-get update
RUN apt-get install -y nginx
RUN echo 'Hi, I am in your container in github' \
        > /var/www/html/index.nginx-debian.html
EXPOSE 80
ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]
