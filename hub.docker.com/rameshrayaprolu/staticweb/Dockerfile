# You can download that file from:                                                                                             
# https://github.com/docker-training/staticweb
FROM ubuntu:14.04
MAINTAINER Docker testing auto build function, ramesh <rayaprolu.ramesh@gmail.com>

RUN apt-get update
RUN apt-get install -y nginx
RUN echo 'Hi, I am in your container' \
    >/usr/share/nginx/html/index.html

CMD [ "nginx", "-g", "daemon off;" ]

EXPOSE 80
