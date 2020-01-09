FROM ubuntu:14.04
MAINTAINER Docker Education Team <education@docker.com>
#testing automated build
RUN apt-get update
RUN apt-get install -y nginx
RUN echo 'Hi, I am in your container' \
    >/usr/share/nginx/html/index.html
#a 2nd test comment
CMD [ "nginx", "-g", "daemon off;" ]

EXPOSE 80
