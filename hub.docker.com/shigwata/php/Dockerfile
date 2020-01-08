FROM php:5

COPY php.ini /usr/local/etc/php/

RUN apt-get update && apt-get install -y \
  git \
  libbz2-dev \
  wget \
  zip \
  && docker-php-ext-install \
  bz2 

# INSTALL COMPOSER
RUN wget -cq https://getcomposer.org/composer.phar -O /usr/local/bin/composer && \
  chmod a+x /usr/local/bin/composer

#INSTALL PHP_CodeSniffer
RUN wget -cq https://squizlabs.github.io/PHP_CodeSniffer/phpcs.phar -O /usr/local/bin/phpcs && \
  chmod a+x /usr/local/bin/phpcs
RUN wget -cq https://squizlabs.github.io/PHP_CodeSniffer/phpcbf.phar -O /usr/local/bin/phpcbf && \
  chmod a+x /usr/local/bin/phpcbf

#INSTALL PHP-CS-FIXER
RUN wget -cq http://get.sensiolabs.org/php-cs-fixer.phar -O /usr/local/bin/php-cs-fixer && \
  chmod a+x /usr/local/bin/php-cs-fixer

#INSTALL PHP MESS DETECTOR
RUN wget -cq http://static.phpmd.org/php/latest/phpmd.phar -O /usr/local/bin/phpmd && \
  chmod a+x /usr/local/bin/phpmd

#INSTALL PHP Copy/Paste Detector
RUN wget -cq https://phar.phpunit.de/phpcpd.phar -O /usr/local/bin/phpcpd && \
  chmod a+x /usr/local/bin/phpcpd

#INSTALL PHP Dead Code Detector
RUN wget -cq https://phar.phpunit.de/phpdcd.phar -O /usr/local/bin/phpdcd && \
  chmod a+x /usr/local/bin/phpdcd

#INSTALL PHPLOC
RUN wget -cq https://phar.phpunit.de/phploc.phar -O /usr/local/bin/phploc && \
  chmod a+x /usr/local/bin/phploc

#INSTALL PHP_Depend
RUN wget -cq http://static.pdepend.org/php/latest/pdepend.phar -O /usr/local/bin/pdepend && \
  chmod a+x /usr/local/bin/pdepend
