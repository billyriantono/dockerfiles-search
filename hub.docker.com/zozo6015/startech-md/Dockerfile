FROM debian:9
MAINTAINER  "StarTech-RD"
USER root

RUN   apt update && apt install -y curl procps net-tools gnupg2

RUN   curl -s http://nginx.org/keys/nginx_signing.key -o - | apt-key add -

RUN   echo "deb http://nginx.org/packages/mainline/debian/ stretch nginx" | tee /etc/apt/sources.list.d/nginx.list && \
      echo "deb-src http://nginx.org/packages/mainline/debian/ stretch nginx" | tee -a /etc/apt/sources.list.d/nginx.list

RUN   apt update && \
      apt -y upgrade && \
      apt -y install php7.0 \
                         php7.0-bcmath \
                         php7.0-bz \
                         php7.0-cli \
                         php7.0-common \
                         php7.0-curl \
                         php7.0-fpm \
                         php7.0-gd \
                         php7.0-mbstring \
                         php7.0-mcrypt \
                         php7.0-mysql \
                         php7.0-readline \
                         php7.0-soap \
                         php7.0-tidy \
                         php7.0-xml \
                         php7.0-xmlrpc \
                         php7.0-zip \
                         sed \
                         curl \
                         nginx

RUN   curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
                               apt install -y nodejs


RUN   npm install pm2@latest -g

RUN   mkdir -p /run/php
RUN   rm -rf /run/php/*

RUN   mkdir -p /var/log/nginx

RUN   sed -i 's/^user.*/user\ =\ nginx/' /etc/php/7.0/fpm/pool.d/www.conf && \
      sed -i 's/^group.*/group\ =\ nginx/' /etc/php/7.0/fpm/pool.d/www.conf && \
      sed -i 's/^listen.owner.*/listen.owner\ =\ nginx/' /etc/php/7.0/fpm/pool.d/www.conf && \
      sed -i 's/^listen.group.*/listen.group\ =\ nginx/' /etc/php/7.0/fpm/pool.d/www.conf

WORKDIR   /root

ADD   ./nginx/apps.yaml /opt/apps.yaml

EXPOSE 80

CMD ["tail", "-f", "/var/log/alternatives.log"]
#ENTRYPOINT   ["pm2", "start", "/opt/apps.yaml", "--no-daemon"]
