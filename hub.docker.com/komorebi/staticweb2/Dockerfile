FROM ubuntu:14.04
MAINTAINER Docker EducationTeams <education@docker.com>

RUN apt-get update
RUN apt-get install -y nginx
RUN echo 'Hi, I am in your container' \
    >/usr/share/nginx/html/index.html
#comment
CMD [ "nginx", "-g", "daemon off;" ]

EXPOSE 80
