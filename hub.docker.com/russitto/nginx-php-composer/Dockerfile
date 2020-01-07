FROM maxexcloo/nginx-php:latest
MAINTAINER Matias Russitto <matias@russitto.com>
RUN apt-get install -y git ssh-client && \
    apt-get clean && \
    cd /bin && wget -O- https://getcomposer.org/installer | php  && \
    mkdir -p /data/http && \
    wget -O /data/http/index.php https://bitbucket.org/russitto/docker-nginx-php-composer/raw/2ca601a64b1c1278df7c402f1718b8d7af1ff3a2/index.php
