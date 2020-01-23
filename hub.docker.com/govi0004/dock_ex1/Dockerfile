# Version: 0.0.1
FROM ubuntu:16.04
MAINTAINER Govardhan Reddy "govi@fb.com"
RUN apt update; apt install -y nginx
RUN echo 'Hi, I am in your container' > /var/www/html/index.html
EXPOSE 80
CMD [ "/bin/bash" ]
