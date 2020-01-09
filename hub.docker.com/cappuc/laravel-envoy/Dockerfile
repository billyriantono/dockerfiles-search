FROM composer

ENV COMPOSER_HOME /app/.composer

ENV PATH /app/.composer/vendor/bin:$PATH

RUN composer global require laravel/envoy

CMD [ "envoy" ]