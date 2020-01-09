FROM serkin/php7-fpm

MAINTAINER p.kegel@sencon.nl

RUN docker-php-ext-install pdo pdo_mysql

RUN apt-get update -y && apt-get install -y libpng-dev

RUN docker-php-ext-install gd

# Install Phalcon 3

RUN git clone --depth=1 -b 3.2.x https://git@github.com/phalcon/cphalcon.git \
 	&& cd cphalcon/build \
  && ./install
RUN echo "extension=phalcon.so" > $PHP_INI_DIR/conf.d/phalcon.ini


# Install Phalcon 3 dev tools

RUN composer global require --dev 'phalcon/devtools:3.2.x-dev' && \
	ln -s ~/.composer/vendor/bin/phalcon.php /usr/bin/phalcon && \
	chmod ugo+x /usr/bin/phalcon

# Done