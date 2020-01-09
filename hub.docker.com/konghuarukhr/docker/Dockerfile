# Version: 0.0.1
FROM ubuntu:12.04
MAINTAINER konghuarukhr "konghuarukhr@163.com"
RUN apt-get update
RUN apt-get install -y nginx
#RUN echo 'Hi, I am in your container' > /usr/share/nginx/html/index.html
EXPOSE 80
ENTRYPOINT ["/usr/sbin/nginx"]
