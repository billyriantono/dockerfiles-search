FROM alledia/lamp

MAINTAINER Alledia <suport@alledia.com>

# Install Composer
ENV COMPOSER_PATH /etc/composer
RUN rm -rf $COMPOSER_PATH \
    && mkdir -p $COMPOSER_PATH \
    && cd $COMPOSER_PATH \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
