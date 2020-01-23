FROM ubuntu:latest
RUN apt-get update
RUN apt-get install -y apache2 && apt-get clean
#ENTRYPOINT ["/usr/sbin/apache2", "-k", "start"]
#ENV APACHE_RUN_USER student
#ENV APACHE_LOG_DIR /var/log/test1
EXPOSE 80
CMD apachect1 -D FOREGROUND
