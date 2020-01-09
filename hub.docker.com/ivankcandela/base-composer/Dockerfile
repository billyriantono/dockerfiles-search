FROM ivankcandela/base-php-cli

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

ENV COMPOSER_HOME /root/composer

#RUN composer global require laravel/lumen-installer
#RUN composer global require laravel/installer

RUN mkdir /data
VOLUME ["/data"]
WORKDIR /data

ENTRYPOINT ["composer"]
