FROM wordpress:php7.3

# set version label
ARG BUILD_DATE
LABEL build_version="Wordpress Container: Build-date:- ${BUILD_DATE}"
LABEL maintainer="Maarten Mol"  

RUN echo '' | pecl install redis
RUN docker-php-ext-enable redis
