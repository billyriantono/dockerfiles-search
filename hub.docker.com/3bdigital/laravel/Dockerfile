FROM dylanlindgren/docker-laravel-phpfpm

# Install deps for wkhtmltopdf
RUN apt-get update -y && \
    apt-get install -y \
    wkhtmltopdf \
    xvfb

ENTRYPOINT ["/usr/sbin/php5-fpm", "-F"]