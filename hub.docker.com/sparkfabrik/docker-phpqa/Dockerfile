FROM composer/composer:1.1-alpine
MAINTAINER Angel Alvarado <eko3alpha>

COPY composer.json /phpqa/
RUN cd /phpqa \
    && composer global require hirak/prestissimo \
    && composer install

ENTRYPOINT ["/phpqa/vendor/edgedesign/phpqa/phpqa"]
CMD ["--help"]
