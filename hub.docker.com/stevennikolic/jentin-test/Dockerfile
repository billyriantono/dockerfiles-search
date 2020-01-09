# Version: 0.0.1
FROM ubuntu:10.04
MAINTAINER Steven Nikolic "steven@nindoo.de"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get install -y curl vim-nox git-core

RUN apt-get install -y php5 php5-cli php5-curl php5-intl
RUN sed -i "s/short_open_tag = Off/short_open_tag = On/" /etc/php5/*/php.ini
RUN sed -i "s/error_reporting = .*$/error_reporting = E_ERROR | E_WARNING | E_PARSE/" /etc/php5/*/php.ini

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN git clone https://github.com/sigma-z/Jentin.git /var/www/Jentin
ADD composer.json /var/www/Jentin/composer.json

RUN cd /var/www/Jentin && composer install --no-interaction

ENTRYPOINT php -v && echo && echo &&  \
	/var/www/Jentin/vendor/bin/phpunit --bootstrap /var/www/Jentin/test/bootstrap.php /var/www/Jentin/test
