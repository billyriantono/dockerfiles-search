FROM metocean/mini-nodejs-consul:v1.0.0
MAINTAINER MetOcean Operations <ops@metocean.co.nz>

RUN apk -U upgrade
RUN apk-install\
  nginx\
  ca-certificates\
  php-fpm\
  php-json\
  php-zlib\
  php-xml\
  php-pdo\
  php-phar\
  php-openssl\
  php-pdo_mysql\
  php-mysqli\
  php-mysql\
  php-curl\
  php-gd\
  php-iconv\
  php-mcrypt\
  postfix\
  wget\
  && mkdir /tmp/nginx\
  && chown -R nginx:nginx /var/lib/nginx\
  && rm /etc/init.d/nginx\
  && rm /etc/init.d/php-fpm
ADD nginx.sh /etc/service/nginx/run
ADD nginxlogforwarder.sh /etc/service/nginxlogforwarder/run
ADD php-fpm.sh /etc/service/php-fpm/run
ADD postfix.sh /etc/service/postfix/run
ADD comodo-rsa-domain-validation-sha-2-w-root.ca-bundle /usr/local/share/ca-certificates
RUN update-ca-certificates
