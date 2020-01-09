# Ubuntu14-PHP5.2.17 Dockerfile
# Version 1.0

FROM ubuntu:14.04

LABEL maintainer="Angel Adames <angelmadames@gmail.com>"

# Set legacy PHP version environment variable
ENV PHPV 5.2.17

# Install required packages to compile PHP
RUN apt-get update -y \
    && apt install -y wget gzip gcc make build-essential \
    libxml2-dev libcurl4-openssl-dev libpcre3-dev libbz2-dev libjpeg-dev \
    libpng12-dev libfreetype6-dev libt1-dev libmcrypt-dev libmhash-dev \
    freetds-dev libmysqlclient-dev unixodbc-dev libxslt1-dev \
    && apt-get clean

# PRevent issue when compiling freetype support
RUN mkdir -pv /usr/include/freetype2/freetype \
    && ln -sf /usr/include/freetype2/freetype.h /usr/include/freetype2/freetype/freetype.h 

# Change to a safe directory
WORKDIR /tmp/

# Copy the PHP_CURL patch
COPY php_curl_patch.diff php_curl_patch.diff

# Get the PHP and PHP-FPM tarballs and apply some patches
RUN wget -c http://museum.php.net/php5/php-$PHPV.tar.bz2 \
    && wget -c http://php-fpm.org/downloads/php-$PHPV-fpm-0.5.14.diff.gz \
    && tar -xvf php-$PHPV.tar.bz2 \
    && gzip -cd php-$PHPV-fpm-0.5.14.diff.gz | patch -d php-$PHPV -p1 \
    && cat /tmp/php_curl_patch.diff | patch -d php-$PHPV -p0

RUN wget -c -t 3 -O ./debian_patches_disable_SSLv2_for_openssl_1_0_0.patch https://bugs.php.net/patch-display.php\?bug_id\=54736\&patch\=debian_patches_disable_SSLv2_for_openssl_1_0_0.patch\&revision=1305414559\&download\=1 \
    && patch -d php-$PHPV -p1 < debian_patches_disable_SSLv2_for_openssl_1_0_0.patch

# Change working directory to php source files dir
WORKDIR /tmp/php-$PHPV

# Compile PHP with the proper CONFIGURE_ARGS
RUN ./configure --prefix=/usr/share/php52 \
    --datadir=/usr/share/php52 \
    --mandir=/usr/share/man \
    --bindir=/usr/bin/php52 \
    --with-libdir=lib/x86_64-linux-gnu \
    --includedir=/usr/include \
    --with-config-file-path=$PHP_HOME/etc \
    --with-config-file-scan-dir=$PHP_HOME/etc/conf.d \
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
    --enable-fastcgi \
    --enable-force-cgi-redirect \
    --enable-fpm \
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
    --with-openssl \
    --with-mysqli \
    --with-kerberos \
    --enable-dbase \
    --with-mysqli=/usr/bin/mysql_config \
    --enable-gd-native-ttf \
    --with-t1lib=/usr \
    --with-freetype-dir=/usr \
    --with-ldap \
    --with-kerberos=/usr \
    --with-unixODBC=shared,/usr \
    --with-imap-ssl \
    --with-mssql \
    --without-sqlite \
    --enable-soap

# Run make install for legacy PHP configured source
RUN make 
RUN make install

# Run some extra commands for PHP-CGI and PHP-FPM
RUN cp sapi/cgi/fpm/php-fpm /etc/init.d/ \
    && chmod +x /etc/init.d/php-fpm
RUN mkdir /usr/share/php52/bin \
    && ln  -s /usr/bin/php52/php-cgi /usr/share/php52/bin/php-cgi

# Copy the recommended php.ini configuration file to lib_dir
RUN cp php.ini-recommended /usr/share/php52/lib/php.ini
