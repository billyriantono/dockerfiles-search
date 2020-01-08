FROM amgrade/php
MAINTAINER Artem Berdyshev "a.berdyshev@amgrade.com"

ENV DEBIAN_FRONTEND noninteractive

# Set timezone and locale.
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get -y update && \
    apt-get -y install \
    curl \
    php5-cli \
    mysql-client \
    git && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean

COPY php.ini /etc/php5/cli/php.ini

ADD run.sh /usr/bin/run.sh
RUN chmod +x /usr/bin/run.sh

WORKDIR /var/www/html

ENTRYPOINT ["/usr/bin/run.sh"]
