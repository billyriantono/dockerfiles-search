FROM bitnami/php-fpm:7.2

LABEL maintainer "Ron van der Molen <ron@wizkunde.nl>"

ARG MEQP_STANDARD=MEQP2
ARG MEQP_SEVERITY=9

ENV MEQP_STANDARD $MEQP_STANDARD
ENV MEQP_SEVERITY $MEQP_SEVERITY

COPY files/auth.json /root/.composer/

# Install required system packages and dependencies
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === '48e3236262b34d30969dca3c37281b3b4bbe3221bda826ac6a9a62d6444cdb0dcd0615698a5cbe587c3f0fe57a54d8f5') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
RUN chmod 755 /usr/local/bin/composer
RUN composer create-project --repository=https://repo.magento.com magento/marketplace-eqp /opt/bitnami/meqp
RUN chmod -R 777 /opt/bitnami/meqp
RUN rm /root/.composer/auth.json

CMD [ "sh", "-c", "/opt/bitnami/meqp/vendor/bin/phpcs /extension --standard=${MEQP_STANDARD} --severity=${MEQP_SEVERITY} --extensions=php,phtml" ]
