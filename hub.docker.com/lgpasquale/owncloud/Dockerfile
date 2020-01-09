FROM owncloud:latest

MAINTAINER LucaPasquale

RUN apt-get update
RUN apt-get install libldap2-dev
RUN docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/
RUN docker-php-ext-install ldap


