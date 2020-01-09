FROM ubuntu:14.04
MAINTAINER Docker Education Team <education@docker.com>

RUN apt-get update
RUN apt-get install -y nginx
RUN echo 'Hi, I am in your container' \
    >/usr/share/nginx/html/index.html
# Add my comment here
CMD [ "nginx", "-g", "daemon off;" ]
# Add another comment here to force 2nd build
EXPOSE 80
