FROM library/ubuntu:xenial

ENV LANG=C.UTF-8

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv E1DD270288B4E6030699E45FA1715D88E1DF1F24 \
 && echo "deb http://ppa.launchpad.net/git-core/ppa/ubuntu xenial main" >> /etc/apt/sources.list \
 && apt-key adv --keyserver keyserver.ubuntu.com --recv 2A47539FA7A4CB0E264BA89081435F664DD35C72 \
 && echo "deb http://ppa.launchpad.net/becrowdy/curl-backport/ubuntu trusty main" >> /etc/apt/sources.list \
 && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927 \
 && echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" >> /etc/apt/sources.list \
 && sed -i '/^# deb-src /s/^# //' /etc/apt/sources.list \
 && apt update \
 && DEBIAN_FRONTEND=noninteractive apt install -y \
      supervisor git-core openssh-client ruby ruby-dev \
      zlib1g libyaml-0-2 libssl1.0.0 libgdbm3 libreadline6 \
      libncurses5 libffi6 libxml2 libxslt1.1 libcurl3 libicu55 \
      curl imagemagick make re2c bison libxml2-dev libssl-dev \
      libbz2-dev libcurl3-dev libdb5.3-dev libjpeg-dev libpng-dev \
      libxpm-dev libfreetype6-dev libgmp3-dev \
      libc-client-dev libldap2-dev libmcrypt-dev libmhash-dev \
      freetds-dev libz-dev libmysqlclient-dev ncurses-dev \
      libpcre3-dev unixodbc-dev postgresql-server-dev-9.5 \
      libsqlite-dev libaspell-dev libreadline6-dev librecode-dev \
      libsnmp-dev libtidy-dev libxslt-dev libgmp10 \
      libgmp-dev libmagickwand-dev mysql-client-5.7 \
      mongodb-org-shell mongodb-org-tools sudo autoconf \
      software-properties-common rsync \
 && DEBIAN_FRONTEND=noninteractive apt-get build-dep -y php7.0 \
 && rm -rf /var/lib/apt/lists/*
RUN ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/include/gmp.h

RUN echo "Host *" > /etc/ssh/ssh_config \
 && echo "    SendEnv LANG LC_*" >> /etc/ssh/ssh_config \
 && echo "    HashKnownHosts yes" >> /etc/ssh/ssh_config \
 && echo "    GSSAPIAuthentication yes" >> /etc/ssh/ssh_config \
 && echo "    GSSAPIDelegateCredentials no" >> /etc/ssh/ssh_config \
 && echo "    StrictHostKeyChecking no" >> /etc/ssh/ssh_config \
 && echo "    UserKnownHostsFile=/dev/null" >> /etc/ssh/ssh_config

RUN gem install capifony && gem install capistrano_rsync_with_remote_cache

RUN adduser --disabled-login --gecos 'PHP' php
RUN echo "php ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# switch user to php
USER php
ENV HOME /home/php
WORKDIR /home/php

# install phpenv
RUN curl https://raw.githubusercontent.com/CHH/phpenv/master/bin/phpenv-install.sh | bash
RUN echo 'export PATH="/home/php/.phpenv/bin:$PATH"' >> /home/php/.bashrc
RUN echo 'eval "$(phpenv init -)"' >> /home/php/.bashrc
RUN mkdir /home/php/.phpenv/plugins; \
    cd /home/php/.phpenv/plugins; \
    git clone https://github.com/php-build/php-build.git

RUN echo '"mongodb","http://pecl.php.net/get/mongodb-$version.tgz","https://github.com/mongodb/mongo-php-driver.git",,,"extension",' >> /home/php/.phpenv/plugins/php-build/share/php-build/extension/definition

ENV PATH /home/php/.phpenv/shims:/home/php/.phpenv/bin:$PATH
ENV PHP_7_0_VERSION 7.0.30
ENV PHP_7_1_VERSION 7.1.21
ENV PHP_7_2_VERSION 7.2.9

RUN CONFIGURE_OPTS="--enable-phar --with-libdir=/lib/x86_64-linux-gnu --with-gmp --enable-intl --with-pear" PHP_BUILD_INSTALL_EXTENSION="apcu=5.1.12 imagick=3.4.3 mongodb=1.5.2" phpenv install $PHP_7_0_VERSION && rm -r /tmp/php-build
RUN CONFIGURE_OPTS="--enable-phar --with-libdir=/lib/x86_64-linux-gnu --with-gmp --enable-intl --with-pear" PHP_BUILD_INSTALL_EXTENSION="apcu=5.1.12 imagick=3.4.3 mongodb=1.5.2" phpenv install $PHP_7_1_VERSION && rm -r /tmp/php-build
RUN CONFIGURE_OPTS="--enable-phar --with-libdir=/lib/x86_64-linux-gnu --with-gmp --enable-intl --with-pear" PHP_BUILD_INSTALL_EXTENSION="apcu=5.1.12 imagick=3.4.3 mongodb=1.5.2" phpenv install $PHP_7_2_VERSION && rm -r /tmp/php-build

RUN cd /home/php/.phpenv/versions \
 && ln -s $PHP_7_0_VERSION 7.0 \
 && ln -s $PHP_7_1_VERSION 7.1 \
 && ln -s $PHP_7_2_VERSION 7.2 \
 && phpenv rehash
