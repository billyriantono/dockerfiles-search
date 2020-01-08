FROM samloh84/centos:7

ARG PRODUCT=php
ARG PRODUCT_VERSION=2.4.1
ARG TEMP_DIR_ROOT=/tmp/${PRODUCT}
ARG TEMP_DIR=/${TEMP_DIR_ROOT}/${PRODUCT_VERSION}
ARG INSTALL_DIR_ROOT=/opt/${PRODUCT}
ARG INSTALL_DIR=${INSTALL_DIR_ROOT}/${PRODUCT_VERSION}

ARG PHP_SRC_TARXZ_URL="http://sg2.php.net/get/php-7.1.6.tar.xz/from/this/mirror"
ARG PHP_SRC_TARXZ=php-7.1.6.tar.xz
ARG PHP_SRC_TARXZ_SHA256SUM=01584dc521ab7ec84b502b61952f573652fe6aa00c18d6d844fb9209f14b245b

ARG PHP_GPG_KEYS="9C0D5763 33CFC8B3"
ARG PHP_SRC_TARXZ_ASC_URL="http://php.net/get/php-7.1.6.tar.xz.asc/from/a/mirror"
ARG PHP_SRC_TARXZ_ASC="php-7.1.6.tar.xz.asc"

USER ${ROOT_UID}

RUN \
PHP_COMPILE_DEPENDENCIES="gcc gcc-c++ autoconf automake make libtool flex bison re2c " && \
PHP_COMPILE_DEPENDENCIES+="libxml2-devel openssl-devel gdbm-devel zlib-devel bzip2-devel " && \
PHP_COMPILE_DEPENDENCIES+="libcurl-devel sqlite-devel pcre-devel gmp-devel gd-devel " && \
PHP_COMPILE_DEPENDENCIES+="libc-client-devel uw-imap-static uw-imap-devel libicu-devel openldap-devel " && \
PHP_COMPILE_DEPENDENCIES+="libmcrypt-devel postgresql-devel aspell-devel readline-devel libedit-devel " && \
PHP_COMPILE_DEPENDENCIES+="net-snmp-devel libtidy-devel libxslt-devel" && \
yum install -y epel-release && \
yum install -y ${PHP_COMPILE_DEPENDENCIES} && \
mkdir -p ${TEMP_DIR} ${INSTALL_DIR} && \
pushd ${TEMP_DIR} && \
curl -LjSs \
${PHP_SRC_TARXZ_URL} -o ${PHP_SRC_TARXZ} && \
curl -LjSs \
${PHP_SRC_TARXZ_ASC_URL} -o ${PHP_SRC_TARXZ_ASC} && \
for PHP_GPG_KEY in ${PHP_GPG_KEYS}; do gpg --keyserver pool.sks-keyservers.net --recv-keys ${PHP_GPG_KEY}; done && \
echo "${PHP_SRC_TARXZ_SHA256SUM}  ${PHP_SRC_TARXZ}" | sha256sum -c - && \
tar -xf ${PHP_SRC_TARXZ} --strip-components=1 -C ${TEMP_DIR} && \
./configure --prefix=${INSTALL_DIR} --with-libdir=lib64 \
--enable-re2c-cgoto \
--enable-fpm \
--enable-phpdbg \
--enable-phpdbg-webhelper \
--with-openssl \
--with-kerberos \
--with-pcre-regex \
--with-pcre-jit \
--with-zlib \
--enable-bcmath \
--with-bz2 \
--enable-calendar \
--with-curl \
--enable-dba \
--with-gdbm \
--enable-exif \
--enable-ftp \
--with-gd \
--enable-gd-native-ttf \
--enable-gd-jis-conv \
--with-gettext \
--with-gmp \
--with-mhash \
--with-imap \
--with-kerberos \
--with-imap-ssl \
--enable-intl \
--with-ldap \
--enable-mbstring \
--with-mcrypt \
--with-mysqli \
--enable-pcntl \
--with-pdo-mysql \
--with-pdo-pgsql \
--with-pgsql \
--with-pspell \
--with-libedit \
--with-readline \
--enable-shmop \
--with-snmp \
--enable-soap \
--enable-sockets \
--enable-sysvmsg \
--enable-sysvsem \
--enable-sysvshm \
--with-tidy \
--enable-wddx \
--with-xmlrpc \
--with-xsl \
--enable-zip \
--enable-mysqlnd \
--with-pear && \
make && \
make install && \
pushd ${INSTALL_DIR} && \
PATH=${INSTALL_DIR}/bin:${PATH} pear upgrade-all && \
popd && \
fix-ownership ${INSTALL_DIR} && \
fix-permissions ${INSTALL_DIR} && \
yum remove -y ${PHP_COMPILE_DEPENDENCIES} && \
yum clean all && \
popd && \
rm -rf ${TEMP_DIR_ROOT}

ENV PHP_HOME ${INSTALL_DIR}
ENV PATH ${PHP_HOME}/bin:${PATH}

USER ${APP_UID}


