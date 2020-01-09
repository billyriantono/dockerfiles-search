FROM quay.io/pantheon-public/build-tools-ci:6.x

USER root

RUN apt-get update && apt-get install -y libxml2-dev \
    && pear install SOAP-0.14.0 \
    && docker-php-ext-install soap;