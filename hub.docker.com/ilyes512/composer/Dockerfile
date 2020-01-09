FROM composer:1.9.0

ENV COMPOSER_HOME /composer
ENV PRESTISSIMO_VERSION 0.3.9

    # install prestissimo composer plugin (paralell downloading of packages - remove this when Composer 2 is released!)
RUN composer global require hirak/prestissimo:$PRESTISSIMO_VERSION \
    && rm -rf /tmp/*
