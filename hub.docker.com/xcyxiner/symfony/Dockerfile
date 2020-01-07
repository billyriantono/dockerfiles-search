#VERSION 0.0.1
#symfony3 基于apache2 php7实现
#FROM nimmis/apache-php7 7.022
FROM mobingi/ubuntu-apache2-php7:7.2
#签名
MAINTAINER xcyxiner "xcyxiner@me.com"
RUN apt-get update
#symfony 初始化必须
RUN apt-get install -y  php-xml
#mongodb php 
RUN apt-get install -y  php-mongodb
#amqp php
RUN apt-get install -y php7.0-mbstring
RUN apt-get install -y php7.0-bcmath
