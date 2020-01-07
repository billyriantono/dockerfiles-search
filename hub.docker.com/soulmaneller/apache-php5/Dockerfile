FROM debian:jessie
MAINTAINER Sitthidet Chaksu <oxoox22@gmail.com>

RUN apt-get update
RUN apt-get install -y locales \
    apache2 \
    php5 \
    php5-cli \
    libapache2-mod-php5 \
    php5-gd \
    php5-json \
    php5-ldap \
    php5-mysql \
    php5-pgsql
RUN apt-get install -y php5-curl \
    php5-redis

COPY scripts/run.sh /scripts/run.sh
RUN chmod +x /scripts/run.sh
RUN a2enmod rewrite

EXPOSE 80
CMD [ "/scripts/run.sh" ]
