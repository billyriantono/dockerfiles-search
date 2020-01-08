FROM php:5.6.29-apache
COPY src/ /var/www/html
RUN a2enmod rewrite

Expose 80

FROM oraclelinux:7-slim 
ENV PACKAGE_URL https://repo.mysql.com/yum/mysql-5.5-community/docker/x86_64/mysql-community-server-minimal-5.5.54-2.el7.x86_64.rpm 

#Install server 

RUN rpmkeys --import http://repo.mysql.com/RPM-GPG-KEY-mysql \
  && yum install -y $PACKAGE_URL \
  && yum install -y libpwquality \
  && rm -rf /var/cache/yum/*
RUN mkdir /docker-entrypoint-initdb.d
VOLUME /var/lib/mysql
#COPY docker-entrypoint.sh /entrypoint.sh
COPY src/ /var/www/html
#ENTRYPOINT ["/entrypoint.sh"]
EXPOSE 3306


