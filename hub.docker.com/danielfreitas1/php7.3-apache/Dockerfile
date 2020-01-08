FROM php:7.3-apache

ENV LC_ALL=C.UTF-8
ENV DEBIAN_FRONTEND=noninteractive
ENV ACCEPT_EULA=Y
ENV TERM=xterm

RUN apt-get purge -y php*
RUN apt-get update

RUN apt-get install -y --no-install-recommends apt-utils
RUN apt-get install -y --no-install-recommends apt-transport-https 
RUN apt-get install -y --no-install-recommends software-properties-common

RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update

RUN apt-get install -y curl 
RUN apt-get install -y git 
RUN apt-get install -y iputils-ping
RUN apt-get install -y libxml2-dev
RUN apt-get install -y libzip-dev
RUN apt-get install -y supervisor 
RUN apt-get install -y unzip
RUN apt-get install -y vim
RUN apt-get install -y zip
RUN apt-get install -y zlib1g-dev

RUN apt-get install -y nodejs
RUN apt-get install -y yarn

RUN docker-php-ext-install bcmath
RUN docker-php-ext-install ctype
RUN docker-php-ext-install json
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install pdo
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install tokenizer
RUN docker-php-ext-install xml
RUN docker-php-ext-install zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer global require hirak/prestissimo

RUN apt-get update 
RUN apt-get clean -y
RUN apt-get autoclean -y
RUN apt-get autoremove -y

RUN a2enmod rewrite

COPY conf/apache/000-default.conf /etc/apache2/sites-available/000-default.conf
COPY conf/apache/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY conf/config /config
COPY conf/run.sh /run.sh

RUN chmod 755 /run.sh

WORKDIR /var/www/html

EXPOSE 80 80

CMD ["/run.sh"]