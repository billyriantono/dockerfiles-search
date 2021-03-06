FROM bitnami/minideb-extras:stretch-r354
LABEL maintainer "Bitnami <containers@bitnami.com>"

# Install required system packages and dependencies
RUN install_packages build-essential autoconf libcurl4-openssl-dev pkg-config libssl-dev ghostscript imagemagick libbz2-1.0 libc6 libcomerr2 libcurl3 libffi6 libfreetype6 libgcc1 libgcrypt20 libgmp10 libgnutls30 libgpg-error0 libgssapi-krb5-2 libhogweed4 libicu57 libidn11 libidn2-0 libjpeg62-turbo libk5crypto3 libkeyutils1 libkrb5-3 libkrb5support0 libldap-2.4-2 liblzma5 libmcrypt4 libmemcached11 libmemcachedutil2 libncurses5 libnettle6 libnghttp2-14 libp11-kit0 libpng16-16 libpq5 libpsl5 libreadline7 librtmp1 libsasl2-2 libsqlite3-0 libssh2-1 libssl1.0.2 libssl1.1 libstdc++6 libsybdb5 libtasn1-6 libtidy5 libtinfo5 libunistring0 libxml2 libxslt1.1 zlib1g
RUN bitnami-pkg unpack php-7.1.28-0 --checksum d42b033c9f897a43d96b1a34c5ebf53472f3c880ae1e3abf39ee361e116cccbe
RUN bitnami-pkg install node-8.16.0-0 --checksum 78a03661720e52ad60e308abcc2ed8576afb3da51b4fb9021252d0ee87fddc8f
RUN bitnami-pkg install laravel-5.8.3-0 --checksum 2e8ceaaf19270ab5bb0002f6b4114644e87720308888c6a7aec18feea4e146a9
RUN mkdir /app && chown bitnami:bitnami /app

COPY rootfs /
ENV BITNAMI_APP_NAME="laravel" \
    BITNAMI_IMAGE_VERSION="5.8.3-debian-9-r48" \
    NODE_PATH="/opt/bitnami/node/lib/node_modules" \
    PATH="/opt/bitnami/php/bin:/opt/bitnami/php/sbin:/opt/bitnami/node/bin:/opt/bitnami/laravel/bin:$PATH"

RUN sudo pecl install mongodb 
RUN sudo bash -c "echo 'extension=mongodb.so' >> /opt/bitnami/php/lib/php.ini"

EXPOSE 3000

WORKDIR /app
USER bitnami
ENTRYPOINT [ "/app-entrypoint.sh" ]
CMD [ "php", "artisan", "serve", "--host=0.0.0.0", "--port=3000" ]
