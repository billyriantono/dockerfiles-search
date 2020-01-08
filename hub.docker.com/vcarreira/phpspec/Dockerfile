FROM vcarreira/composer

MAINTAINER "Vitor Carreira" <vitor.carreira@gmail.com>

RUN mkdir -p /opt/packages

WORKDIR /opt/packages

RUN composer require phpspec/phpspec

WORKDIR /var/www

VOLUME /var/www

ENTRYPOINT ["/opt/packages/vendor/bin/phpspec"]
CMD ["--help"]
