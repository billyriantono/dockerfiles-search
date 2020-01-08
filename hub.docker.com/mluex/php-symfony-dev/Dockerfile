FROM mluex/php-dev:7.2

RUN wget https://get.symfony.com/cli/installer -O - | bash && \
    mv /root/.symfony/bin/symfony /usr/local/bin/symfony

WORKDIR /home/wwwroot/

EXPOSE 9000
CMD ["php-fpm"]