FROM ubuntu:16.04

#Workaround to enable nano
ENV	TERM xterm

ENV	DEBIAN_FRONTEND noninteractive

COPY	root/* /root/
RUN	chmod +x /root/set_php_version.sh

RUN apt-get update && apt-get install -y --no-install-recommends \
    wget nano patch curl \
    apache2 \
    gcc make build-essential \
    libxml2-dev \
    libcurl4-openssl-dev \
    libpcre3-dev \
    libbz2-dev libjpeg-dev \
    libpng12-dev \
    libfreetype6-dev \
    libmcrypt-dev \
    libmhash-dev \
    freetds-dev \
    libxslt1-dev \
    libssl-dev \
    libltdl-dev \
    libbz2-dev \
    software-properties-common \
    libpng-dev \
    libmysqlclient-dev \
    php-cli \
    php-mysql \
    php-xml \
    php-mbstring \
    php-gd \
    php-curl \
    zip \
    unzip \
    openssh-server \
    mysql-client

COPY etc /etc

RUN a2enmod cgid actions rewrite

################ Install php 5.2 ################

RUN curl -L -s https://museum.php.net/php5/php-5.2.17.tar.gz | tar -xvz -C /tmp

RUN wget -qO- https://downloads.mysql.com/archives/get/file/mysql-5.1.72-linux-x86_64-glibc23.tar.gz | tar -xvz -C /tmp

RUN curl -s https://mail.gnome.org/archives/xml/2012-August/txtbgxGXAvz4N.txt | patch -d /tmp/php-5.2.17 -p0 # patch libxml because version > 2.9

WORKDIR /tmp/php-5.2.17

RUN  ./configure \
    --prefix=/usr/share/php5.2 \
    --datadir=/usr/share/php5.2 \
    --mandir=/usr/share/man \
    --bindir=/usr/bin/php5.2 \
    --with-libdir=lib/x86_64-linux-gnu \
    --includedir=/usr/include \
    --with-config-file-path=/etc/php/5.2/apache2/ \
    --with-config-file-scan-dir=/etc/php/5.2/conf.d \
    --disable-debug \
    --with-regex=php \
    --disable-rpath \
    --disable-static \
    --disable-posix \
    --with-pic \
    --with-layout=GNU \
    --with-pear=/usr/share/php \
    --enable-calendar \
    --enable-sysvsem \
    --enable-sysvshm \
    --enable-sysvmsg \
    --enable-bcmath \
    --with-bz2 \
    --enable-ctype \
    --without-gdbm \
    --with-iconv \
    --enable-exif \
    --enable-ftp \
    --enable-cli \
    --with-gettext \
    --enable-mbstring \
    --with-pcre-regex \
    --enable-shmop \
    --enable-sockets \
    --enable-wddx \
    --with-mcrypt \
    --with-zlib \
    --enable-pdo \
    --with-curl \
    --enable-inline-optimization \
    --enable-xml \
    --enable-pcntl \
    --enable-mbregex \
    --with-mhash \
    --with-xsl \
    --enable-zip \
    --with-gd \
    --with-pdo-mysql \
    --with-jpeg-dir=/usr/lib \
    --with-png-dir=/usr/lib \
    --with-mysql=/tmp/mysql-5.1.72-linux-x86_64-glibc23/bin/mysql_config \
    --enable-gd-native-ttf \
    --with-freetype-dir=/usr \
    --enable-soap

RUN make && make install

RUN mkdir -p /var/www/html/cgi/php-5.2 && \
    ln -s /usr/bin/php5.2/php-cgi /var/www/html/cgi/php-5.2/

RUN mkdir -p /etc/php/5.2/apache2/ && cp /tmp/php-5.2.17/php.ini-dist /etc/php/5.2/apache2/php.ini
RUN sed -i "s/upload_max_filesize = .*/upload_max_filesize = 10M/" /etc/php/5.2/apache2/php.ini

################ Install php 5.3 ################
RUN curl -L -s https://museum.php.net/php5/php-5.3.29.tar.gz | tar -xvz -C /tmp
WORKDIR /tmp/php-5.3.29
RUN ./configure \
    --prefix=/usr/share/php5.3 \
    --datadir=/usr/share/php5.3 \
    --mandir=/usr/share/man \
    --bindir=/usr/bin/php5.3 \
    --with-libdir=lib/x86_64-linux-gnu \
    --includedir=/usr/include \
    --with-config-file-path=/etc/php/5.3/apache2/ \
    --with-config-file-scan-dir=/etc/php/5.3/conf.d \
    --disable-debug \
    --with-regex=php \
    --disable-rpath \
    --disable-static \
    --disable-posix \
    --with-pic \
    --with-layout=GNU \
    --with-pear=/usr/share/php \
    --enable-calendar \
    --enable-sysvsem \
    --enable-sysvshm \
    --enable-sysvmsg \
    --enable-bcmath \
    --with-bz2 \
    --enable-ctype \
    --without-gdbm \
    --with-iconv \
    --enable-exif \
    --enable-ftp \
    --enable-cli \
    --with-gettext \
    --enable-mbstring \
    --with-pcre-regex \
    --enable-shmop \
    --enable-sockets \
    --enable-wddx \
    --with-mcrypt \
    --with-zlib \
    --enable-pdo \
    --with-curl \
    --enable-inline-optimization \
    --enable-xml \
    --enable-pcntl \
    --enable-mbregex \
    --with-mhash \
    --with-xsl \
    --enable-zip \
    --with-gd \
    --with-pdo-mysql \
    --with-jpeg-dir=/usr/lib \
    --with-png-dir=/usr/lib \
    --with-mysql=/tmp/mysql-5.1.72-linux-x86_64-glibc23/bin/mysql_config \
    --enable-gd-native-ttf \
    --with-freetype-dir=/usr \
    --enable-soap

RUN make && make install

RUN mkdir -p /var/www/html/cgi/php-5.3 && \
    ln -s /usr/bin/php5.3/php-cgi /var/www/html/cgi/php-5.3/

RUN mkdir -p /etc/php/5.3/apache2/ && cp /tmp/php-5.3.29/php.ini-development /etc/php/5.3/apache2/php.ini
RUN sed -i "s/upload_max_filesize = .*/upload_max_filesize = 10M/" /etc/php/5.3/apache2/php.ini

################ Install php 5.4 ################
RUN curl -s https://museum.php.net/php5/php-5.4.45.tar.gz | tar -xvz -C /tmp
WORKDIR /tmp/php-5.4.45
RUN ./configure \
    --prefix=/usr/share/php5.4 \
    --datadir=/usr/share/php5.4 \
    --mandir=/usr/share/man \
    --bindir=/usr/bin/php5.4 \
    --with-libdir=lib/x86_64-linux-gnu \
    --includedir=/usr/include \
    --with-config-file-path=/etc/php/5.4/apache2/ \
    --with-config-file-scan-dir=/etc/php/5.4/conf.d \
    --disable-debug \
    --with-regex=php \
    --disable-rpath \
    --disable-static \
    --disable-posix \
    --with-pic \
    --with-layout=GNU \
    --with-pear=/usr/share/php \
    --enable-calendar \
    --enable-sysvsem \
    --enable-sysvshm \
    --enable-sysvmsg \
    --enable-bcmath \
    --with-bz2 \
    --enable-ctype \
    --without-gdbm \
    --with-iconv \
    --enable-exif \
    --enable-ftp \
    --enable-cli \
    --with-gettext \
    --enable-mbstring \
    --with-pcre-regex \
    --enable-shmop \
    --enable-sockets \
    --enable-wddx \
    --with-mcrypt \
    --with-zlib \
    --enable-pdo \
    --with-curl \
    --enable-inline-optimization \
    --enable-xml \
    --enable-pcntl \
    --enable-mbregex \
    --with-mhash \
    --with-xsl \
    --enable-zip \
    --with-gd \
    --with-pdo-mysql \
    --with-jpeg-dir=/usr/lib \
    --with-png-dir=/usr/lib \
    --with-mysql \
    --enable-gd-native-ttf \
    --with-freetype-dir=/usr \
    --enable-soap

RUN make && make install

RUN mkdir -p /var/www/html/cgi/php-5.4 && \
    ln -s /usr/bin/php5.4/php-cgi /var/www/html/cgi/php-5.4/

RUN mkdir -p /etc/php/5.4/apache2/ && cp /tmp/php-5.4.45/php.ini-development /etc/php/5.4/apache2/php.ini
RUN sed -i "s/upload_max_filesize = .*/upload_max_filesize = 10M/" /etc/php/5.4/apache2/php.ini


################ Install php 5.5 ################
RUN curl -s https://museum.php.net/php5/php-5.5.38.tar.gz | tar -xvz -C /tmp
WORKDIR /tmp/php-5.5.38
RUN ./configure \
    --prefix=/usr/share/php5.5 \
    --datadir=/usr/share/php5.5 \
    --mandir=/usr/share/man \
    --bindir=/usr/bin/php5.5 \
    --with-libdir=lib/x86_64-linux-gnu \
    --includedir=/usr/include \
    --with-config-file-path=/etc/php/5.5/apache2/ \
    --with-config-file-scan-dir=/etc/php/5.5/conf.d \
    --disable-debug \
    --with-regex=php \
    --disable-rpath \
    --disable-static \
    --disable-posix \
    --with-pic \
    --with-layout=GNU \
    --with-pear=/usr/share/php \
    --enable-calendar \
    --enable-sysvsem \
    --enable-sysvshm \
    --enable-sysvmsg \
    --enable-bcmath \
    --with-bz2 \
    --enable-ctype \
    --without-gdbm \
    --with-iconv \
    --enable-exif \
    --enable-ftp \
    --enable-cli \
    --with-gettext \
    --enable-mbstring \
    --with-pcre-regex \
    --enable-shmop \
    --enable-sockets \
    --enable-wddx \
    --with-mcrypt \
    --with-zlib \
    --enable-pdo \
    --with-curl \
    --enable-inline-optimization \
    --enable-xml \
    --enable-pcntl \
    --enable-mbregex \
    --with-mhash \
    --with-xsl \
    --enable-zip \
    --with-gd \
    --with-pdo-mysql \
    --with-jpeg-dir=/usr/lib \
    --with-png-dir=/usr/lib \
    --with-mysql=mysqlnd \
    --with-mysqli=mysqlnd \
    --enable-gd-native-ttf \
    --with-freetype-dir=/usr \
    --enable-soap

RUN make && make install

RUN mkdir -p /var/www/html/cgi/php-5.5 && \
    ln -s /usr/bin/php5.5/php-cgi /var/www/html/cgi/php-5.5/

RUN mkdir -p /etc/php/5.5/apache2/ && cp /tmp/php-5.5.38/php.ini-development /etc/php/5.5/apache2/php.ini
RUN sed -i "s/upload_max_filesize = .*/upload_max_filesize = 10M/" /etc/php/5.5/apache2/php.ini

################ Install recent php versions ################

RUN LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php
RUN apt-get update && apt-get install -y --no-install-recommends \
  php5.6-cgi \
  php5.6-mysql \
  php5.6-xml \
  php5.6-gd \
  php7.0-cgi \
  php7.0-mysql \
  php7.0-xml \
  php7.0-gd \
  php7.1-cgi \
  php7.1-mysql \
  php7.1-xml \
  php7.1-gd \
  php7.2-cgi \
  php7.2-mysql \
  php7.2-xml \
  php7.2-gd \
  php7.3-cgi \
  php7.3-mysql \
  php7.3-xml \
  php7.3-gd \
  php-mysql

RUN mkdir /var/www/html/cgi/php-5.6 && ln -s /usr/bin/php-cgi5.6 /var/www/html/cgi/php-5.6/php-cgi
RUN mkdir /var/www/html/cgi/php-7.0 && ln -s /usr/bin/php-cgi7.0 /var/www/html/cgi/php-7.0/php-cgi
RUN mkdir /var/www/html/cgi/php-7.1 && ln -s /usr/bin/php-cgi7.1 /var/www/html/cgi/php-7.1/php-cgi
RUN mkdir /var/www/html/cgi/php-7.2 && ln -s /usr/bin/php-cgi7.2 /var/www/html/cgi/php-7.2/php-cgi
RUN mkdir /var/www/html/cgi/php-7.3 && ln -s /usr/bin/php-cgi7.3 /var/www/html/cgi/php-7.3/php-cgi

RUN /root/set_php_version.sh 7.2

RUN rm -rf /tmp/*

RUN sed -i 's/^Port .*/Port 2222/g' /etc/ssh/sshd_config
RUN sed -i 's/^PermitRootLogin .*/PermitRootLogin yes/g' /etc/ssh/sshd_config

RUN echo "root:password" | chpasswd

COPY usr/local/bin/ /usr/local/bin/
RUN rm -rf /var/lib/apt/lists/*

RUN chmod +x /usr/local/bin/docker_entrypoint.sh /usr/local/bin/apache2_foreground.sh

WORKDIR /var/www/html

ENTRYPOINT ["docker_entrypoint.sh"]
CMD ["apache2_foreground.sh"]
