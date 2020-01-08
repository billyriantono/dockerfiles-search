FROM vixns/php-nginx:7
MAINTAINER Stéphane Cottin <stephane.cottin@vixns.com>
WORKDIR /data/htdocs

RUN apt-get update && \
  apt-get install --no-install-recommends -y ssmtp libmysqlclient-dev mysql-client && \
  rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install mysqli

RUN curl -o /usr/local/bin/wp https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
chmod 755 /usr/local/bin/wp

ENV DB_HOST mysql

COPY config/php /usr/local/etc/php-fpm.d
COPY config/nginx /etc/nginx/conf.d

COPY run.sh /run.sh
CMD ["/run.sh"]
