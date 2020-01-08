FROM edbizarro/gitlab-ci-pipeline-php:7.3

USER root
WORKDIR /tmp

# Install GMP
RUN apt-get update && apt-get install -y libgmp-dev
RUN ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/include/gmp.h
RUN docker-php-ext-install gmp

WORKDIR /var/www/html