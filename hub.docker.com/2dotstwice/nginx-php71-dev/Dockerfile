FROM 2dotstwice/nginx-php71-starter

# PHP configuration for development
RUN sed -i -e "s/opcache.validate_timestamps=0/opcache.validate_timestamps=1/g" ${PHP_CONFIG_DIR}/fpm/conf.d/99-custom.ini