FROM marceloalmeida/php-docker:latest

MAINTAINER Marcelo Almeida <marcelo.almeida@jumia.com>

WORKDIR "/root"

ENV DEBIAN_FRONTEND noninteractive
ENV VERSION 1.7.0
ENV LIBRABBITC_VERSION 0.7.1

# INSTALL BUILDER DEPENDENCIES
RUN apt-get update && apt-get install -y --no-install-recommends \
  apt-utils \
  build-essential \
  checkinstall \
  libc6-dev \
  libssl-dev \
  lsb-release \
  make \
  php7.0-dev \
  re2c \
  runawk \
  wget

COPY src /src

# INSTALL PACKAGES DEPENDENCIES
RUN mkdir /pkg
RUN wget https://github.com/alanxz/rabbitmq-c/releases/download/v$LIBRABBITC_VERSION/rabbitmq-c-$LIBRABBITC_VERSION.tar.gz ;\
  tar -zxvf rabbitmq-c-$LIBRABBITC_VERSION.tar.gz ;\
  cd rabbitmq-c-$LIBRABBITC_VERSION ;\
  ./configure --prefix=/usr ;\
  make ;\
  make install

# CREATE PACKAGE
RUN wget -q https://pecl.php.net/get/amqp-$VERSION.tgz ;\
  tar -zxvf amqp-$VERSION.tgz ;\
  cd amqp-$VERSION ;\
  cp -r /src/* /root/amqp-$VERSION/. ;\
  phpize ;\
  ./configure LIBS=/usr/lib/librabbitmq.so.4 ;\
  checkinstall -y --install=no --pkgname='php7.0-amqp' --pkgversion='$VERSION-aig' --pkggroup='php' --pkgsource='https://github.com/pdezwart/php-amqp' --maintainer='Marcelo Almeida \<marcelo.almeida@jumia.com\>' --requires='php7.0-common \(\>= 7.0.7\), librabbitmq1 \(\>= $LIBRABBITC_VERSION\)' --include=include_etc

VOLUME ["/pkg"]
