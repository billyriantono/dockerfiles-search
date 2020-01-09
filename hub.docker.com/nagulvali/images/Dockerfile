#This image is based on cnetos7 and will start apache server

FROM centos:latest
MAINTAINER nagulvali.aws@gmail.com

RUN yum update -y
RUN yum install -y httpd net-tools

RUN echo "This is custom index file build during image creation" > /var/www/html/index.html
EXPOSE 80

ENTRYPOINT apachectl "-DFOREGROUND" 


