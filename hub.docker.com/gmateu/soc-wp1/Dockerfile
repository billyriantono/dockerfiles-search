FROM wordpress:apache

RUN apt-get update && apt-get install -y libcurl4-openssl-dev libldb-dev libldap2-dev
RUN ln -s /usr/lib/x86_64-linux-gnu/libldap.so /usr/lib/libldap.so \
  && ln -s /usr/lib/x86_64-linux-gnu/liblber.so /usr/lib/liblber.so
RUN docker-php-ext-install curl \
  && docker-php-ext-configure ldap \
  && docker-php-ext-install ldap
