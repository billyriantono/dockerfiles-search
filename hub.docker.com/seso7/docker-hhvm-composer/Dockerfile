FROM diegomarangoni/hhvm

RUN apt-get update -y && \
    apt-get install -y curl git && \
    curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    composer self-update && \
    apt-get remove --purge curl -y && \
    apt-get clean

EXPOSE 9000

WORKDIR /var/data/www

CMD ["hhvm", "--mode=server"]