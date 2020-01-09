FROM php:5.6-fpm

LABEL maintainer = "wickedvikingstudios@gmail.com" \
      vendor = "wickedviking" \
      description = "PHP 5.6 FPM" \
      licence = "MIT" \
      documentation= "https://github.com/wickedviking/php56"

ADD assets /assets
RUN chmod +x /assets/*.sh \
    && /assets/provision.sh

EXPOSE 9000
CMD ["php-fpm"]