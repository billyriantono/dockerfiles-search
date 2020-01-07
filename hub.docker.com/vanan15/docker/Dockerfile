# A basic apache server. To use either add or bind mount content under /var/www
FROM ubuntu:12.04

MAINTAINER An Dinh version: 0.5

RUN apt-get update && apt-get install -y apache2 git && apt-get clean && rm -rf /var/lib/apt/lists/* \
&& cd /var \
&& git clone https://github.com/vanan15/testrepo.git \
&& cd testrepo \
&& rm -rf /var/www \
&& ln -sf `pwd`/public /var/www

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

EXPOSE 80

CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]
