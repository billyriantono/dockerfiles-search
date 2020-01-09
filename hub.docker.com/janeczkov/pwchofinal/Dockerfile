FROM ubuntu
EXPOSE 80
RUN apt-get update
RUN apt-get install apache2
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
