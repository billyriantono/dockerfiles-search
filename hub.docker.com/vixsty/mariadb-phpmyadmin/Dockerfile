#utilisation de debian comme base (plus léger que ubuntu)
FROM debian:jessie

MAINTAINER LARQUEMIN Kevin "kevin@oosp.fr"

# Définition des variables d'environnement
ENV PMA_SECRET blowfish_secret
ENV PMA_USERNAME pmauser
ENV PMA_PASSWORD PWpmaD1

ENV MYSQL_TCP_ADDR db
ENV MYSQL_TCP_PORT 3306
ENV MYSQL_ROOT_USERNAME root
ENV MYSQL_ROOT_PASSWORD routes

ENV PMA_VERSION 4.7.0
ENV MAX_UPLOAD "50M"

ENV PMA_WORKING_DIR /var/www/pma

# Installation des outils de base
# besoin app
RUN apt-get update
RUN	apt-get install -y curl nginx php5-fpm php5-mysql mysql-client \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Installation de phpmyadmin
RUN curl https://files.phpmyadmin.net/phpMyAdmin/${PMA_VERSION}/phpMyAdmin-${PMA_VERSION}-all-languages.tar.gz | tar xvz \
	&& rm -rvf /var/www \
	&& mkdir -p /var/www \
	&& mv phpMyAdmin-${PMA_VERSION}-all-languages ${PMA_WORKING_DIR}\
	&& chown -R www-data: ${PMA_WORKING_DIR}

# Configuration du vhost nginx pour notre application
RUN rm -rvf /etc/nginx/sites-enabled/default
ADD config/pma.conf /etc/nginx/sites-enabled/

# Montage ou copie des fichiers et des scripts de configuration PMA et App
# RUN rm -vf ${PMA_WORKING_DIR}/config.inc.php
ADD config/config.inc.php ${PMA_WORKING_DIR}/
ADD config/create_user.sql /
ADD config/pma-start /usr/local/bin/
ADD config/pma-firstrun /usr/local/bin/

RUN chmod +x /usr/local/bin/pma-start
RUN chmod +x /usr/local/bin/pma-firstrun

# Changement des variables dans les configurations nginx et php
RUN sed -i "s/http {/http {\n        client_max_body_size $MAX_UPLOAD;/" /etc/nginx/nginx.conf
RUN sed -i -e 's|^listen =.*$|listen = 127.0.0.1:9000|' etc/php5/fpm/pool.d/www.conf
RUN sed -i "s/upload_max_filesize = 2M/upload_max_filesize = $MAX_UPLOAD/" /etc/php5/fpm/php.ini
RUN sed -i "s/post_max_size = 8M/post_max_size = $MAX_UPLOAD/" /etc/php5/fpm/php.ini

# Ouverture du port externe 80 pour un accès en dehors du container
EXPOSE 80

# forward request logs to Docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

# exécution du script de démarrage.
CMD ["pma-start"]
