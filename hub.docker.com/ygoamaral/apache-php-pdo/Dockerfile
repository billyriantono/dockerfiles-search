FROM php:7.1-apache

ENV LD_LIBRARY_PATH=/opt/oracle/instantclient_12_1

ENV ORACLE_HOME=/opt/oracle/instantclient_12_1

RUN apt-get update \
  && apt-get install --no-install-recommends -y \
  wget \
  gnupg \
  memcached \
  apt-utils \
  libpq-dev \
  libaio-dev \
  libpng-dev \
  freetds-dev \
  libmcrypt-dev \
  libfreetype6-dev \
  libmemcached-dev \
  libjpeg62-turbo-dev
# possiveis instalações
# g++ \
# openssl \
# zlib1g-dev \
# libicu-dev \
# libssl-dev \
# libxml2-dev \
# unixodbc-dev \
# libpng12-dev

RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main" > /etc/apt/sources.list.d/pgdg.list \
  && wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | \
  apt-key add -

RUN apt-get update \
  && apt-get install --no-install-recommends -y \
  postgresql-server-dev-9.6 \
  supervisor \
  && mkdir /opt/oracle

COPY ./instantclient_12_1.tar.xz /opt/oracle

COPY ./supervisord.conf /etc/supervisor/conf.d

COPY ./memcached.conf /etc/supervisor/conf.d

COPY ./apache2.conf /etc/supervisor/conf.d

RUN cd /opt/oracle \
  # && echo '=== Download instant client - 40.2 MB ===' \
  # && wget -O instantclient_12_1.tar.xz --quiet https://doc-0s-3k-docs.googleusercontent.com/docs/securesc/a60d33kkpue5dcsf8afhtvcl9uoc4lsu/u5dl30bsp8d6darbp0fuvhjo8km91m75/1567771200000/03287997780401191551/03287997780401191551/13fQKvw__5CF8Srte5WBAOkl462yCLBdb?e=download&nonce=lbi9tf3hg665i&user=03287997780401191551&hash=ff98dor9vdj8j7dv1j673qin0j35u3p0
  && tar xf instantclient_12_1.tar.xz \
  && rm -f instantclient_12_1.tar.xz \
  && ln -s /opt/oracle/instantclient_12_1/libocci.so.12.1 /opt/oracle/instantclient_12_1/libocci.so \
  && ln -s /opt/oracle/instantclient_12_1/libclntsh.so.12.1 /opt/oracle/instantclient_12_1/libclntsh.so \
  && ln -s /opt/oracle/instantclient_12_1/libclntshcore.so.12.1 /opt/oracle/instantclient_12_1/libclntshcore.so

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && pecl install memcached \
  && docker-php-ext-configure pdo_oci --with-pdo-oci=instantclient,/opt/oracle/instantclient_12_1,12.1 \
  && docker-php-ext-configure pdo_dblib --with-libdir=/lib/x86_64-linux-gnu \
  && docker-php-ext-install -j$(nproc) \
  gd \
  zip \
  mcrypt \
  pdo_oci \
  mbstring \
  pdo_dblib \
  pdo_mysql \
  pdo_pgsql \
  && docker-php-ext-enable \
  memcached

RUN curl -s https://getcomposer.org/installer | php \
  && mv composer.phar /usr/local/bin/composer

RUN apt-get clean -y \
  && apt-get remove -y \
  && apt-get autoclean -y \
  && apt-get autoremove -y

CMD ["/usr/bin/supervisord"]