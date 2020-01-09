FROM mariadb
MAINTAINER 33ASO

ENV MYSQL_USER root
ENV MYSQL_DATABASE magento
ENV MYSQL_ROOT_PASSWORD 123

ADD ./magento.sql /docker-entrypoint-initdb.d
