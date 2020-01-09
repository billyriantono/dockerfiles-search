# Version: 0.0.1
FROM ubuntu:16.04
MAINTAINER Collin Hayden "collin@collinhayden.com"
ENV REFRESHED_AT 2018-10-15
RUN apt-get update; apt-get install -y nginx
RUN apt-get install -y vim
RUN echo "Hi, I am a container running locally on latest" >/var/www/html/index.html
EXPOSE 80
ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]
