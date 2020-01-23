# Baixa a imagem do ubuntu
FROM ubuntu:xenial
LABEL maintainer="Higor Martins <higgor.m@gmail.com>"

# Instalação dos pacotes
RUN \
apt-get update && \
apt-get install -y python-software-properties software-properties-common && \
LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php && \
apt-get update && apt-get install -y \
apache2 \
php5.6 \
php5.6-cli \
php5.6-common \
php5.6-gd \
php5.6-json \
php5.6-ldap \
php5.6-mysql \
php5.6-pgsql \
php5.6-apcu \
php5.6-imagick \
php5.6-mcrypt \
php5.6-sybase \
php5.6-xdebug \
curl \
phpunit \
nano \
git \
zip \
unzip \
&& apt-get clean && apt-get autoclean && apt-get autoremove \
&& rm -rf /var/lib/apt/lists/*

# Habilita o modo de reescrita do apache
RUN a2enmod rewrite

ENV APACHE_LOCK_DIR="/var/lock"
ENV APACHE_PID_FILE="/var/run/apache2.pid"
ENV APACHE_RUN_USER="www-data"
ENV APACHE_RUN_GROUP="www-data"
ENV APACHE_LOG_DIR="/var/log/apache2"

LABEL Description="Webserver php 5.6.37"

VOLUME /var/www/html

ENV TZ=America/Sao_Paulo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Copia o arquivo de virtualhost
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

# Install composer
WORKDIR /usr/local/bin/
RUN curl -sS https://getcomposer.org/installer | php
RUN chmod +x composer.phar
RUN mv composer.phar composer
RUN composer self-update

# Set path bin
WORKDIR /root
RUN echo 'export PATH="$PATH:$HOME/.composer/vendor/bin"' >> ~/.bashrc

WORKDIR /var/www/html

COPY apache2-foreground.sh /scripts/
RUN chmod +x /scripts/*

EXPOSE 80

CMD ["/scripts/apache2-foreground.sh"]

# Install PHPCodeSniffer
RUN composer global require "squizlabs/php_codesniffer=2.*"
RUN chmod u+x ~/.composer/vendor/bin/phpcs
RUN chmod u+x ~/.composer/vendor/bin/phpcbf

#Configuration at PhpCompatibility
WORKDIR ~/.composer/vendor/squizlabs/php_codesniffer/CodeSniffer/Standards
RUN git clone https://github.com/wimg/PHPCompatibility.git

WORKDIR ~/.composer/vendor/bin
RUN ~/.composer/vendor/bin/phpcs --config-set installed_paths  ~/.composer/vendor/squizlabs/php_codesniffer/CodeSniffer/Standards/PHPCompatibility
RUN ~/.composer/vendor/bin/phpcs --config-set error_severity 1
RUN ~/.composer/vendor/bin/phpcs --config-set warning_severity 0
