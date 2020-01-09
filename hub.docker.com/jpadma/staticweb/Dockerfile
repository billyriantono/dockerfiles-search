FROM ubuntu:14.04
MAINTAINER Docker Education Team <education@docker.com> #jpadma

RUN apt-get update
RUN apt-get install -y nginx
RUN echo 'Hi, Jal am in your container' \
    >/usr/share/nginx/html/index.html

CMD [ "nginx", "-g", "daemon off;" ]

EXPOSE 80
