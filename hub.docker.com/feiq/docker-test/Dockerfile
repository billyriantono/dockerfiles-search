FROM ubuntu
MAINTAINER FeiQ "feiqing.zjf@gmail.com"
RUN apt-get update
RUN apt-get install -y nginx
RUN echo 'Hi, I am container FeiQ' > /var/www/html/index.nginx-debian.html
RUN touch /root/test.txt
RUN echo 'automatend' > /root/test.txt
RUN echo 'hh'
EXPOSE 80
