# Version 0.0.1
FROM ubuntu:14.04
MAINTAINER Mao Le "maole@example.local"
RUN apt-get update && \
    apt-get install -y nginx && \
    echo "Hello guys, I am in your container" >/usr/share/nginx/html/index.html
EXPOSE 80
