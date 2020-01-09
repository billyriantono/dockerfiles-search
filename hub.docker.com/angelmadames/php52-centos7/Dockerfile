# Centos7-PHP5.2.17 Dockerfile
# Version 1.0

FROM centos:7

LABEL maintainer="Angel Adames <angelmadames@gmail.com>"

# Set legacy PHP version environment variable
ENV PHPV 5.2.17

# Install required packages to compile PHP
RUN yum install -y epel-release \
    && yum update -y \
    && yum install -y wget bzip2 patch gcc gettext-devel make libtool libxml2-devel \
    pcre-devel zlib-devel openssl-devel libxslt-devel libpng-devel libXpm-devel \
    libc-client-devel libmcrypt-devel curl-devel expat-devel libjpeg-devel \
    libmhash libmhash-devel krb5-devel freetype-devel sqlite-devel mysql-devel aspell-devel \
    && yum clean all

# Clean orphaned repos
RUN rm -rf /var/cache/yum

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

# Soft-link the lib and include directories to avoid dependencies issues
# when compiling legacy PHP version.
RUN ln -s /usr/include /opt/include \
    && ln -s /usr/lib64 /opt/lib

# Change working directory to php source files dir
WORKDIR /tmp/php-$PHPV

# Compile PHP with the proper CONFIGURE_ARGS
RUN ./configure --prefix=/usr/local --enable-fastcgi --enable-fpm --enable-cli \
	--enable-fpm --enable-cli --enable-bcmath --enable-calendar \
	--enable-exif --enable-ftp --enable-gd-native-ttf \
	--enable-libxml --with-libxml-dir=/opt/include/libxml2 \
	--enable-magic-quotes --enable-mbstring \
	--enable-pdo=shared --enable-soap --enable-sockets \
	--enable-sqlite-utf8 --enable-wddx --enable-zip \
	--with-curl --with-freetype-dir=/opt/include/freetype2 \
	--with-gd --with-gettext --with-jpeg-dir=/opt \
	--with-kerberos --with-libexpat-dir=/opt --with-mcrypt=/opt \
	--with-mime-magic --with-mysql=/opt --with-mysqli \
	--with-openssl --with-pcre-regex --with-pdo-mysql=shared \
	--with-pdo-sqlite=shared --with-png-dir=/opt --with-pspell \
	--with-sqlite=shared --with-ttf --with-xmlrpc --with-xpm-dir=/opt \
	--with-xsl=/opt/include/libxslt/ --with-zlib --with-zlib-dir=/opt

# Run make install for legacy PHP configured source
RUN make all install

# Run some extra commands for PHP-CGI and PHP-FPM
RUN strip /usr/local/bin/php-cgi \
    && cp sapi/cgi/fpm/php-fpm /etc/init.d/ \
    && chmod +x /etc/init.d/php-fpm

# Copy the recommended php.ini configuration file to lib_dir
RUN cp php.ini-recommended /usr/local/lib/php.ini

# Installing extra PHP extensions using PECL
RUN echo "" | /usr/local/bin/pecl install apc-3.1.9 \
    && echo "" | /usr/local/bin/pecl install timezonedb-2012.3 \
    && echo "" | /usr/local/bin/pecl install mongo-1.4.5
