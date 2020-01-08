FROM debian

MAINTAINER Diogo Costa <diogo.fe.costa@gmail.com>

RUN apt-get update && apt-get install -y perl pwgen --no-install-recommends && rm -rf /var/lib/apt/lists/*
RUN apt-key adv --keyserver ha.pool.sks-keyservers.net --recv-keys A4A9406876FCBD3C456770C88C718D3B5072E1F5

ENV MYSQL_MAJOR 5.7
ENV MYSQL_VERSION 5.7.12-1debian8

RUN echo "deb http://repo.mysql.com/apt/debian/ jessie mysql-${MYSQL_MAJOR}" > /etc/apt/sources.list.d/mysql.list

ENV DEBIAN_FRONTEND noninteractive

RUN alias adduser='useradd' && apt-get update && apt-get install -y mysql-server supervisor wget unzip sudo htop

RUN apt-get -y install openssh-server

# Setup the supervisor run template
ADD ./docker/mysql.conf /etc/supervisor/conf.d/mysql.conf
ADD ./docker/start.sh /start.sh
ADD ./docker/mysql-bindaddress.cnf /etc/mysql/conf.d/bindaddress.cnf
RUN chmod 755 /start.sh

RUN /etc/init.d/mysql start && mysql -u root --execute="create database sonar; grant all on sonar.* to sonar identified by 'MabwHu2jMTp';"

VOLUME /var/lib/mysql

EXPOSE 3306 9000 22

CMD ["/bin/bash", "/start.sh"]
