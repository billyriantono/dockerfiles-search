FROM wordpress
LABEL maintainer "Research and Innovation Co.,Ltd. <sdd@r-n-i.jp>"

RUN apt-get update && \
    apt-get install -y libpng-dev && \
    docker-php-ext-install gd && \
    a2enmod headers && \
    a2enmod ext_filter
