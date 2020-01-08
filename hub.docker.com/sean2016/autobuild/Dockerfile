#Version:0.0.1
FROM ubuntu:14.04
MAINTAINER sean "caizhenzhen2010@xx.com"
RUN apt-get update
RUN apt-get install -y nginx
RUN echo 'HI, I am in your container'\
        >/usr/share/nginx/html/index.html
EXPOSE 80
