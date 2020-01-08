FROM wordpress:latest

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils
RUN apt-get install git -y
RUN apt-get install vim -y
RUN apt-get install curl -y
RUN apt-get install --only-upgrade openssl -y
RUN apt-get install --only-upgrade libssl-dev -y
RUN apt-get install libcurl4-gnutls-dev -y
RUN apt-get install libldap2-dev -y
RUN rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/
RUN docker-php-ext-install curl ldap