FROM ubuntu:14.04
MAINTAINER Docker Education Team <education@docker.com>

#comment
RUN apt-get update
RUN apt-get install -y nginx curl
RUN echo 'Hi, I am in your container' \
    >/usr/share/nginx/html/index.html

CMD [ "nginx", "-g", "daemon off;" ]

EXPOSE 80
