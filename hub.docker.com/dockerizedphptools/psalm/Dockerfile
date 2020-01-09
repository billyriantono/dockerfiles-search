FROM php:7.4-cli-alpine

WORKDIR /app

# Install composer
RUN wget https://raw.githubusercontent.com/composer/getcomposer.org/76a7060ccb93902cd7576b67264ad91c8a2700e2/web/installer -O - -q | php -- --quiet

RUN php composer.phar global require vimeo/psalm

ENTRYPOINT ["/root/.composer/vendor/bin/psalm"]
