###################################################
#      PHP / PHP 7.0.1-fpm
###################################################

FROM debian:jessie

MAINTAINER Pascha Butretell <admin@pascha.domains>

#==================================================
#    ENV VARIABLES / POST INSTALLATION
#==================================================

# Change this value to force a full image rebuild
ENV    IMAGE_VERSION "2016-01-07"

# Skip all post-install configurations steps
ENV    DEBIAN_FRONTEND "noninteractive"

# Set the new user/group with fixed uid/gid
ENV    MASTER_USER "pascha"
ENV    MASTER_GROUP "pascha"
ENV    MASTER_UID "3342"
ENV    MASTER_GID "3342"

# Set the system language
ENV    SYS_LANGUAGE "en_US.UTF-8"
RUN    export LANGUAGE=${SYS_LANGUAGE} \
    && export LC_ALL=${SYS_LANGUAGE} \
    && export LANG=${SYS_LANGUAGE}
    
# Set the timezone
ENV    TIMEZONE "Europe/Zurich"

# Define PHP details
ENV    PHP_VERSION "7.0.1"
ENV    PHP_MD5 "2da2981724d5c99ab7dc6e2164c8e756"
ENV    PHP_INI_DIR "/volumes/php-conf"
ENV    FPM_CONF_DIR "/volumes/php-conf"

# PHP key
RUN    gpg --keyserver ha.pool.sks-keyservers.net --recv-keys 1A4E8B7277C42E53DBA9C7B9BCAA30EA9C0D5763

#==================================================
#    CREATE USERS / GROUPS
#==================================================

# Create user and group with predefined UID and GID
RUN    groupadd -g ${MASTER_GID} -r ${MASTER_GROUP} \
    && useradd -u ${MASTER_UID} -m -r -g ${MASTER_GID} ${MASTER_USER}
    
#==================================================
#      REPOSITORIES
#==================================================    

# Add default repositories
RUN    echo ' \
             deb http://ftp.ch.debian.org/debian/ jessie main\n \
             deb http://security.debian.org/ jessie/updates main\n \
             deb http://ftp.ch.debian.org/debian/ jessie-updates main\n \
             deb http://http.debian.net/debian jessie-backports main\n \
             ' \ 
       > /etc/apt/sources.list

# Add specific repositories
# ...

#==================================================
#      INSTALLATIONS / CONFIGURATIONS
#==================================================

#      INSTALL PREREQUISITES
#--------------------------------------------------

RUN    apt-get update \
    && apt-get install -y \
       --no-install-recommends \
       locales ca-certificates \
    && echo ${TIMEZONE} > /etc/timezone \
    && dpkg-reconfigure tzdata \
    && locale-gen ${SYS_LANGUAGE} \
    && dpkg-reconfigure locales

#      INSTALL TOOLS / LIBS
#--------------------------------------------------

RUN    apt-get update \
    && apt-get install -y \
       --no-install-recommends \
       curl g++ make

    
#      INSTALL APPLICATIONS
#--------------------------------------------------

RUN    apt-get update \
    && apt-get install -y \
       --no-install-recommends \
       libcurl4-openssl-dev libreadline6-dev librecode-dev \
       libsqlite3-dev libssl-dev libxml2-dev xz-utils \
       libpng-dev libicu-dev libmcrypt-dev libpq-dev pkg-config \
    && cd /tmp \
    && mkdir -p /usr/src/php \
    && mkdir -p "${PHP_INI_DIR}/conf.d" \
    && mkdir -p "${FPM_CONF_DIR}/" \
    && curl -fSL "http://php.net/get/php-${PHP_VERSION}.tar.gz/from/this/mirror" -o "php.tar.gz" \
    && curl -fSL "http://php.net/get/php-${PHP_VERSION}.tar.gz.asc/from/this/mirror" -o "php.tar.gz.asc" \
    && gpg --verify php.tar.gz.asc \
    && echo "${PHP_MD5} php.tar.gz" | md5sum -c \
    && tar -xzf php.tar.gz -C /usr/src/php --strip-components=1 \
    && cd /usr/src/php \
    && ./configure \
        --disable-cli \
        --enable-fpm \
        --with-fpm-user=${MASTER_USER} \
        --with-fpm-group=${MASTER_GROUP} \
        --disable-cgi \
        --with-config-file-path="${PHP_INI_DIR}" \
        --with-config-file-scan-dir="${PHP_INI_DIR}/conf.d" \
        --disable-ipv6 \
        --with-openssl \
        --with-pcre-regex \
        --with-zlib \
        --enable-calendar \
        --with-curl \        
        --enable-exif \ 
        --with-gd \
        --with-gettext \
        --enable-intl \
        --enable-mbstring \
        --with-mcrypt \
        --with-pdo-mysql \
        --with-pdo-pgsql \
        --with-pgsql \
        --with-readline \
        --with-recode \
        --enable-soap \
        --enable-zip \
        --enable-mysqlnd \
        --with-pear \
    && make --jobs="$(nproc)" \
    && make install \
    && { find /usr/local/bin /usr/local/sbin -type f -executable -exec strip --strip-all '{}' + || true; } \
    && make clean

#   CONFIGURE APPLICATIONS
#--------------------------------------------------


#==================================================
#    UNINSTALL / CLEANUP
#==================================================

RUN    apt-get autoremove --purge -y \
       ca-certificates pkg-config g++ make \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/*
    
#==================================================
#    OTHER STUFF
#==================================================

EXPOSE 9000

ADD    docker-entrypoint.sh /
RUN    chown ${MASTER_USER}:${MASTER_GROUP} /docker-entrypoint.sh \
    && chmod 550 /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["-y","${FPM_CONF_DIR}/php-fpm.conf"]