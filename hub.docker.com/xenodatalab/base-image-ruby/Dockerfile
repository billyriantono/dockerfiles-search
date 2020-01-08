FROM ubuntu:18.04

MAINTAINER xenodata lab., Inc. <development@xenodata-lab.com>

RUN apt-get update -y \
  && apt-get install -y \
    language-pack-ja \
    gcc \
    make \
    autoconf \
    openssl \
    zlib1g-dev \
    libssl-dev \
    libreadline-dev \
    g++ \
    curl \
    wget \
    git

ENV LC_CTYPE=ja_JP.utf8 \
    LANG=ja_JP.utf8 \
    RUBY_MAJOR=2.7 \
    RUBY_VERSION=2.7.0 \
    RUBY_DOWNLOAD_SHA256=27d350a52a02b53034ca0794efe518667d558f152656c2baaf08f3d0c8b02343 \
    RUBYGEMS_VERSION=3.1.2 \
    BUNDLER_VERSION=2.1.4

# skip installing gem documentation
RUN mkdir -p /usr/local/etc \
  && { \
    echo 'install: --no-document'; \
    echo 'update: --no-document'; \
  } >> /usr/local/etc/gemrc \
  # some of ruby's build scripts are written in ruby
  #   we purge system ruby later to make sure our final image uses what we just built
  && set -ex \
  \
  && buildDeps=' \
    bison \
    dpkg-dev \
    libgdbm-dev \
    ruby \
  ' \
  && apt-get update \
  && apt-get install -y --no-install-recommends $buildDeps \
  && rm -rf /var/lib/apt/lists/* \
  \
  && wget -O ruby.tar.xz "https://cache.ruby-lang.org/pub/ruby/${RUBY_MAJOR%}/ruby-$RUBY_VERSION.tar.xz" \
  && echo "$RUBY_DOWNLOAD_SHA256 *ruby.tar.xz" | sha256sum -c - \
  \
  && mkdir -p /usr/src/ruby \
  && tar -xJf ruby.tar.xz -C /usr/src/ruby --strip-components=1 \
  && rm ruby.tar.xz \
  \
  && cd /usr/src/ruby \
  \
  # hack in "ENABLE_PATH_CHECK" disabling to suppress:
  #   warning: Insecure world writable dir
  && { \
    echo '#define ENABLE_PATH_CHECK 0'; \
    echo; \
    cat file.c; \
  } > file.c.new \
  && mv file.c.new file.c \
  \
  && autoconf \
  && gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
  && ./configure \
    --build="$gnuArch" \
    --disable-install-doc \
    --enable-shared \
  && make -j "$(nproc)" \
  && make install \
  \
  && apt-get purge -y --auto-remove $buildDeps \
  && cd / \
  && rm -r /usr/src/ruby \
  \
  && gem update --system "$RUBYGEMS_VERSION" \
  && gem install bundler --version "$BUNDLER_VERSION" --force

CMD ["/bin/bash"]
