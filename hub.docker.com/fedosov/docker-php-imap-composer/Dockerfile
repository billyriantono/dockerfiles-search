FROM alledia/lamp

MAINTAINER Mikhail Fedosov <tbs.micle@gmail.com>

# Install Composer
ENV COMPOSER_PATH /etc/composer
RUN rm -rf $COMPOSER_PATH \
    && mkdir -p $COMPOSER_PATH \
    && cd $COMPOSER_PATH \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN apt-get update -yqq && \
    apt-get install -yqq php5-imap && \
    php5enmod imap
