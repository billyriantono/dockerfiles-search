FROM eviweb/base-image:0.1.1

MAINTAINER Eric VILLARD <dev@eviweb.fr>

RUN add-pack \
        # @main
        libxml2@main \
        libbz2@main \
        libxau@main \
        libxdmcp@main \
        libxcb@main \
        libx11@main \
        libxext@main \
        libice@main \
        libgcc@main \
        libuuid@main \
        libsm@main \
        libxt@main \
        libxpm@main \
        libpng@main \
        freetype@main \
        libjpeg-turbo@main \
        libwebp@main \
        libintl@main \
        libressl2.4-libcrypto@main \
        libressl2.4-libssl@main \
        c-client@main \
        libstdc++@main \
        icu-libs@main \
        db@main \
        libsasl@main \
        libldap@main \
        libmcrypt@main \
        mariadb-common@main \
        mariadb-client-libs@main \
        libpq@main \
        sqlite-libs@main \
        aspell-libs@main \
        libgpg-error@main \
        libgcrypt@main \
        libxslt@main \

        # @community
        php7@community \
        php7-bz2@community \
        php7-common@community \
        php7-ctype@community \
        php7-curl@community \
        php7-dev@community \
        php7-dom@community \
        php7-gd@community \
        php7-gettext@community \
        php7-iconv@community \
        php7-imap@community \
        php7-intl@community \
        php7-json@community \
        php7-ldap@community \
        php7-mbstring@community \
        php7-mcrypt@community \
        php7-mysqli@community \
        php7-mysqlnd@community \
        php7-openssl@community \
        php7-pcntl@community \
        php7-pdo@community \
        php7-pdo_mysql@community \
        php7-pdo_pgsql@community \
        php7-pdo_sqlite@community \
        php7-pgsql@community \
        php7-phar@community \
        php7-phpdbg@community \
        php7-pspell@community \
        php7-session@community \
        php7-sqlite3@community \
        php7-xml@community \
        php7-xmlreader@community \
        php7-xmlrpc@community \
        php7-xsl@community \
        php7-zip@community \
        php7-zlib@community \

        # @testing
        php7-ssh2@testing \
        php7-uuid@testing \
        php7-xdebug@testing \

    && ln -s /usr/bin/php7 /usr/bin/php

ENTRYPOINT ["entrypoint", "php"]
