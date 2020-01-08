FROM alpine:3.8

LABEL maintainer "Ben Roberts <ben@headsnet.com>"

COPY scripts /scripts

RUN /scripts/install-packages.sh && \
    /scripts/ensure-www-data.sh && \
    apk --no-cache add php7-fpm && \
    rm -rf /scripts

COPY www.conf /etc/php7/php-fpm.d/www.conf
COPY php.ini /etc/php7/conf.d/99_app.ini

# Add handy aliases
RUN { \
        echo "alias ls='ls --color=auto'"; \
        echo "alias ll='ls --color=auto -alF'"; \
        echo "alias la='ls --color=auto -A'"; \
        echo "alias l='ls --color=auto -CF'"; \
    } >> ~/.bashrc

WORKDIR /var/www/app

EXPOSE 9000

CMD ["php-fpm7"]
