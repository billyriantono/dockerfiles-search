FROM php:7.2-fpm

# For running APT in non-interactive mode
ENV DEBIAN_FRONTEND noninteractive

# Define build requirements, which can be removed after setup from the container
ENV PHPIZE_DEPS \
  autoconf            \
  build-essential     \
  file                \
  g++                 \
  gcc                 \
  libbz2-dev          \
  libc-client-dev     \
  libc-dev            \
  libcurl4-gnutls-dev \
  libedit-dev         \
  libfreetype6-dev    \
  libgmp-dev          \
  libicu-dev          \
  libjpeg62-turbo-dev \
  libkrb5-dev         \
  libmcrypt-dev       \
  libpng-dev          \
  libpq-dev           \
  libsqlite3-dev      \
  libssh2-1-dev       \
  libxml2-dev         \
  libxslt1-dev        \
  make                \
  pkg-config          \
  re2c

# Set Debian sources
RUN \
  apt-get update && apt-get install -q -y --no-install-recommends wget gnupg apt-transport-https && \
  echo "deb https://deb.nodesource.com/node_8.x stretch main" > /etc/apt/sources.list.d/node.list &&      \
      wget --quiet -O - https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add - &&           \
  echo 'deb http://apt.newrelic.com/debian/ newrelic non-free' > /etc/apt/sources.list.d/newrelic.list && \
      wget -O- https://download.newrelic.com/548C16BF.gpg | apt-key add -

#Fixing the postgresql-client installation issue
RUN mkdir -p /usr/share/man/man7/ && touch /usr/share/man/man7/ABORT.7.gz.dpkg-tmp && \
    mkdir -p /usr/share/man/man1/ && touch /usr/share/man/man1/psql.1.gz

# Install Debian packages
RUN apt-get -qy update && apt-get install -q -y --no-install-recommends $PHPIZE_DEPS \
    nano                \
    iproute2            \
    ca-certificates     \
    curl                \
    debconf             \
    debconf-utils       \
    graphviz            \
    libedit2            \
    libpq5              \
    netcat              \
    nodejs              \
    patch               \
    postgresql-client   \
    psmisc              \
    python-dev          \
    python-setuptools   \
    redis-tools         \
    ssmtp               \
    supervisor          \
    unzip               \
    vim                 \
    wget                \
    zip                 \
  && mkdir /var/run/sshd  \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
  && docker-php-ext-install -j$(nproc) \
        bcmath      \
        bz2         \
        gd          \
        gmp         \
        iconv       \
        intl        \
        mbstring    \
        opcache     \
        pdo         \
        pdo_pgsql   \
        pgsql       \
        readline    \
        soap        \
        sockets     \
        xmlrpc      \
        zip         \
  && pecl install -o -f redis \
  && rm -rf /tmp/pear \
  && echo "extension=redis.so" > $PHP_INI_DIR/conf.d/docker-php-ext-redis.ini \
  && apt-get -qy autoremove \
  && apt-get -qy purge $PHPIZE_DEPS \
  && apt-get -qy autoremove

# create the project dir
RUN mkdir -p /project