FROM ubuntu:16.04
MAINTAINER Iliya Strakovich "iliya@strakovich.com"
RUN apt-get -qq update
RUN apt-get install -qq -y apache2
RUN apt-get install -qq -y curl
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
EXPOSE 80
ONBUILD ADD . /var/www/
ENTRYPOINT ["/usr/sbin/apache2"]
CMD ["-D", "FOREGROUND"]
HEALTHCHECK --interval=10s --timeout=1m --retries=5 CMD curl http://127.0.0.1 || exit 1
