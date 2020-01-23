FROM ubuntu:14.04
MAINTAINER Jose Manuel Hernandez (josemhb@gmail.com)

#Install necesary packages
RUN apt-get update \
  && apt-get install -y apache2 php5 php5-mysqlnd aspell \
  && apt-get clean

#Attach volume for persistent data
VOLUME /var/www/html

#Apache port 80
EXPOSE 80

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
