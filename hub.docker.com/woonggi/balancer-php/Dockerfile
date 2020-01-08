FROM rester/rester-docker
MAINTAINER Woong-Gi Jeon<jeon.wbbi@gmail.com>

RUN mkdir /var/www/cfg
RUN mkdir /var/www/src

ADD cfg /var/www/cfg
ADD src /var/www/src

ADD nginx-conf/default.conf /etc/nginx/sites-available/default.conf
ADD nginx-conf/default-ssl.conf /etc/nginx/sites-available/default-ssl.conf