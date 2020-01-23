FROM alpine:3.8

LABEL maintainer "Ben Roberts <ben@headsnet.com>"

ENV TZ=Europe/Paris

# |--------------------------------------------------------------------------
# | Install PHP and required extensions
# |--------------------------------------------------------------------------

COPY scripts /scripts

RUN /scripts/install-packages.sh && \
    /scripts/install-dev-packages.sh && \
    pecl install amqp && \
    echo 'extension=amqp.so' >> /etc/php7/conf.d/00_amqp.ini && \
    rm -rf /scripts && \
    cp /usr/share/zoneinfo/$TZ /etc/localtime && \
    echo $TZ > /etc/timezone

COPY www.conf /etc/php7/php-fpm.d/www.conf
COPY php.ini /etc/php7/conf.d/99_app.ini

#RUN echo "nameserver 8.8.8.8" >> /etc/resolve.conf
#RUN echo "nameserver 8.8.4.4" >> /etc/resolve.conf

# |--------------------------------------------------------------------------
# | Create user and group for app to run as
# |--------------------------------------------------------------------------

# Create app user with sudo privileges
RUN addgroup -g 1000 -S app && \
    adduser -u 1000 -S app -G app

#     && \
#    adduser app wheel
#
## Users in the sudoers group can sudo as root without password.
#RUN echo '%wheel ALL=(ALL) ALL' >> /etc/sudoers

# |--------------------------------------------------------------------------
# | Install Composer and required plugins
# |--------------------------------------------------------------------------

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

USER app

# This improves performance by allowing parallel downloading
RUN composer global require hirak/prestissimo --no-plugins --no-scripts

# This allows local development of packages symlinked to filesystem
RUN composer global require 'gossi/composer-localdev-plugin=dev-master'

USER root

# Create cache dirs owned by app user, so we can mount our volumes against them
USER app
RUN mkdir -p /home/app/.cache/yarn/v1
RUN mkdir -p /home/app/.composer/cache
USER root

# |--------------------------------------------------------------------------
# | Configure Bash aliases and other developer friendly fixes
# |--------------------------------------------------------------------------

USER app
RUN { \
        echo "alias ls='ls --color=auto'"; \
        echo "alias ll='ls --color=auto -alF'"; \
        echo "alias la='ls --color=auto -A'"; \
        echo "alias l='ls --color=auto -CF'"; \
    } >> ~/.bashrc
USER root
RUN { \
        echo "alias ls='ls --color=auto'"; \
        echo "alias ll='ls --color=auto -alF'"; \
        echo "alias la='ls --color=auto -A'"; \
        echo "alias l='ls --color=auto -CF'"; \
    } >> ~/.bashrc

# |--------------------------------------------------------------------------
# | Finalise the container configuration
# |--------------------------------------------------------------------------

WORKDIR /var/www/app

EXPOSE 9000

CMD ["php-fpm7"]

USER app
