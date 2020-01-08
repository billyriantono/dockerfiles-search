FROM ubuntu
RUN apt-get update
RUN apt-get -y install apache2
expose 80
cmd /usr/sbin/apache2ctl -D FOREGROUND
