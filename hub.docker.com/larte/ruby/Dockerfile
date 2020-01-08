# Dockerfile for larte:ruby/2.1
FROM larte/base
MAINTAINER larte <lauri.arte@gmail.com>

RUN  apt-get install -q -y \
  curl \
  patch \
  bzip2 \
  gawk \
  g++ \
  gcc \
  make \
  libc6-dev \
  patch \
  libreadline6-dev \
  zlib1g-dev \
  libssl-dev \
  libyaml-dev \
  libsqlite3-dev \
  sqlite3 \
  autoconf \
  libgdbm-dev \
  libncurses5-dev \
  automake \
  libtool \
  bison \
  pkg-config \
  libffi-dev

# Install Ruby 2.1.1
RUN mkdir /tmp/ruby && cd /tmp/ruby &&  \
  curl http://ftp.ruby-lang.org/pub/ruby/2.1/ruby-2.1.1.tar.gz | tar xz && \
  cd ruby-2.1.1 && \
  ./configure --disable-install-rdoc --prefix=/usr/local --enable-shared --disable-install-doc --with-opt-dir=/usr/local/lib --with-openssl-dir=/usr --with-readline-dir=/usr --with-zlib-dir=/usr && \
  make && \
  make install && \
  rm -rf /tmp/ruby

# Install bundler gem
RUN gem install bundler --no-ri --no-rdoc
