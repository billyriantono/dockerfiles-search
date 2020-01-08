FROM chialab/php:7.3-apache
RUN a2enmod rewrite
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update
RUN apt-get install nano