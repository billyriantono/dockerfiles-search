FROM ubuntu:14.04
MAINTAINER Docker Education Team <education@docker.com>
# adding comment
RUN apt-get update
RUN apt-get install -y nginx
RUN echo 'Hi, I am in your (training) container' \
    >/usr/share/nginx/html/index.html
# adding comment
CMD [ "nginx", "-g", "daemon off;" ]
# adding comment
EXPOSE 80
# adding comment
