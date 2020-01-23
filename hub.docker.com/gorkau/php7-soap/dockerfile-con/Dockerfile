FROM oraclelinux:7.5

MAINTAINER Gopi Krishna

ENV DEBIAN_FRONTEND noninteractive

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

RUN yum update -y && yum install -y httpd
RUN rm -r /etc/httpd/conf/httpd.conf

COPY ./httpd.conf /etc/httpd/conf/httpd.conf
 
EXPOSE 80

CMD ["httpd"]
