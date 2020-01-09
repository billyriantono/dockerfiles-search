FROM phpdockerio/php71-fpm:latest

# Install selected extensions and other stuff
RUN apt-get update \
    && apt-get -y --no-install-recommends install  php7.1-phpdbg php-memcached php7.1-mysql php7.1-pgsql php-redis php7.1-sqlite3 php7.1-bcmath php7.1-bz2 php7.1-enchant php7.1-gd php7.1-gmp php7.1-imap php7.1-intl php7.1-mbstring php7.1-pspell php7.1-soap php-ssh2 php7.1-tidy php7.1-xsl php-yaml php-xdebug php-zmq \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*
