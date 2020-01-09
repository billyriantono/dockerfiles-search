# You can download that file from:                                                                                             
# https://github.com/docker-training/staticweb
FROM ubuntu:14.04
MAINTAINER Docker Education Team 123<education@docker.com>

RUN apt-get update
RUN apt-get install -y nginx
RUN echo 'Hi, I am in your container 123' \
    >/usr/share/nginx/html/index.html

CMD [ "nginx", "-g", "daemon off;" ]

EXPOSE 80
