# docker build --tag dadyzeus/php7:0.1 --tag dadyzeus/php7:latest .
# docker run -it --rm dadyzeus/php7:0.1 bash
FROM ubuntu
MAINTAINER SungYong EOM <bluei@blueiblog.com>

# 레포지트 업데이트
RUN apt-get update -y

# 타임존 셋팅
RUN apt-get install -y tzdata
RUN ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime

# 기본 패키지 설치
RUN apt install -y gcc make telnet whois vim git gettext cron mysql-client iputils-ping net-tools wget curl net-tools

# PHP 설치
RUN apt install -y php php-cli php-mysql php-pear php-mbstring php-curl php-gd php-imagick php-memcache php-xmlrpc php-geoip
RUN curl -sS https://getcomposer.org/installer -o composer-setup.php
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN rm composer-setup.php
RUN mkdir /php

WORKDIR /php
