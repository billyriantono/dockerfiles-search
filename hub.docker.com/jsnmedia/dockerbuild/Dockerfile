FROM ubuntu:16.04
MAINTAINER Park Jong Seok
LABEL purpose="HandsOnLab"
RUN apt-get update
RUN apt-get install apache2 -y
WORKDIR /var/www/html
RUN ["/bin/bash", "-c", "echo welcome to docker automated!!! >> test.html"]
EXPOSE 80
CMD ["apachectl", "-DFOREGROUND"]