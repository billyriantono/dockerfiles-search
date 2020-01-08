ARG PHP_EXTENSIONS="mysql mysqli pdo_mysql gd imap"
FROM thecodingmachine/php:7.3-v2-apache-node8

# docker image build -t abc . && docker run -p 5000:5000 abc

ENV APP_ENV=prod \
  APACHE_DOCUMENT_ROOT=public/ \
  ABSOLUTE_APACHE_DOCUMENT_ROOT=/var/www/html/public \
  PORT=5000 \
  PHP_EXTENSION_MYSQL=1 \
  PHP_EXTENSION_MYSQLI=1 \
  PHP_EXTENSION_PDO_MYSQL=1 \
  DB_NAME=dbname \
  DB_USER=dbuser \
  DB_PASS=dbpass

EXPOSE 5000

COPY / /var/www/html/
#COPY .env.staging /var/www/html/.env

USER root

RUN  DEBIAN_FRONTEND=noninteractive apt-get install -y software-properties-common dirmngr \
  && curl -sS https://downloads.mariadb.com/MariaDB/mariadb_repo_setup | sudo bash \
  && apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install --allow-unauthenticated -y mariadb-common mariadb-server mariadb-client

RUN sudo sed -i "s/80/$PORT/g" /etc/apache2/sites-available/000-default.conf /etc/apache2/ports.conf 
#  && chown -R docker:docker /var/www \
#  && chmod -R 777 /var/www/html/storage \
#  && composer update 

RUN sudo /bin/bash -c "/usr/bin/mysqld_safe &" \
  && sleep 10s  \
  && sudo mysql -e "CREATE DATABASE $DB_NAME; CREATE USER $DB_USER@localhost IDENTIFIED BY '$DB_PASS'; GRANT ALL PRIVILEGES ON $DB_NAME.* TO '$DB_USER'@'localhost'; FLUSH PRIVILEGES;" 

CMD sudo /bin/bash -c "/usr/bin/mysqld_safe &" \
  && sleep 10s  \
  && sudo /bin/bash entrypoint.sh \
  && apache2-foreground   

