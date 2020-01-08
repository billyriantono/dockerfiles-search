FROM levkov/base:latest
MAINTAINER levkov

RUN apt-get update && apt-get install -y mysql-server-5.5 &&\
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY conf/mysql.conf /etc/supervisor/conf.d/mysql.conf
