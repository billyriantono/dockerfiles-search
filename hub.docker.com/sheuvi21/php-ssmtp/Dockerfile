FROM php:7.1

RUN apt-get update && apt-get install -y ssmtp

RUN cp $PHP_INI_DIR/php.ini-development $PHP_INI_DIR/php.ini
RUN echo 'sendmail_path = /usr/sbin/ssmtp -t' >> $PHP_INI_DIR/php.ini

RUN echo 'FromLineOverride=yes' >> /etc/ssmtp/ssmtp.conf
