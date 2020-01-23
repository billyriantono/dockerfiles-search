FROM bitnami/minideb-extras:stretch-r494
LABEL maintainer "Bitnami <containers@bitnami.com>"

# Install required system packages and dependencies (this is from standard bitnami wordpress)
RUN install_packages libbz2-1.0 libc6 libcomerr2 libcurl3 libexpat1 libffi6 libfreetype6 libgcc1 libgcrypt20 libgmp10 libgnutls30 libgpg-error0 libgssapi-krb5-2 libhogweed4 libicu57 libidn11 libidn2-0 libjpeg62-turbo libk5crypto3 libkeyutils1 libkrb5-3 libkrb5support0 libldap-2.4-2 liblzma5 libmemcached11 libmemcachedutil2 libncurses5 libnettle6 libnghttp2-14 libp11-kit0 libpcre3 libpng16-16 libpq5 libpsl5 libreadline7 librtmp1 libsasl2-2 libsqlite3-0 libssh2-1 libssl1.0.2 libssl1.1 libstdc++6 libsybdb5 libtasn1-6 libtidy5 libtinfo5 libunistring0 libxml2 libxslt1.1 libzip4 zlib1g

# Install custom additionla packages (this is customized for FSB)
RUN install_packages unzip

# Install Apache / Mysql (client)
RUN bitnami-pkg unpack apache-2.4.41-4 --checksum 496e9cc3e12fd38832aae5dc1873cb4593666e6146379f55b2312908917eb666
RUN bitnami-pkg unpack mysql-client-10.3.21-0 --checksum 19c6b964f289772a4e5963e22929133fa65222f66752eb29af715ce3d0b7ef0e

# NOTE: if you change / upgrade the php version you must update / change the ionCube version on the tfc-init.sh script
RUN bitnami-pkg unpack php-7.3.13-0 --checksum 5e55d9741383f32ea8fadfbeae5a6fd9b86f188c67e9839e26449f80dd3addef
RUN bitnami-pkg install libphp-7.3.13-2 --checksum cdad3af7b23f54dbcf13818651979d7f23324c6092e5bde760eee1be1a740346

# Started copy of scripts files ...
COPY scripts /
# Finished copy of scripts files

# Load up env variables ...
ENV ALLOW_EMPTY_PASSWORD="no" \
    BITNAMI_APP_NAME="freshstore" \
    BITNAMI_IMAGE_VERSION="5.3.2-debian-9-r17" \
    PATH="/opt/bitnami/apache/bin:/opt/bitnami/php/bin:/opt/bitnami/php/sbin:/opt/bitnami/mysql/bin:$PATH" \
    MARIADB_HOST="mariadb" \
    MARIADB_PORT_NUMBER="3306" \
    MARIADB_ROOT_PASSWORD="" \
    MARIADB_ROOT_USER="root" \
    MYSQL_CLIENT_CREATE_DATABASE_NAME="" \
    MYSQL_CLIENT_CREATE_DATABASE_PASSWORD="" \
    MYSQL_CLIENT_CREATE_DATABASE_PRIVILEGES="ALL" \
    MYSQL_CLIENT_CREATE_DATABASE_USER="" \
    DATABASE_NAME="bitnami_fsb" \
    DATABASE_PASSWORD="" \
    DATABASE_USER="bn_fsb" \
    FSB_TABLE_PREFIX="fsb_" \
    FSB_FORCE_CLEANUP="no" \
    FSB_FORCE_REINSTALL="no"
# Finished loading up env variables

# Started copy of vhost files ...
COPY conf /opt/bitnami/apache/conf/vhosts/
# Finished copy of vhost files

# Adjust script permissions
RUN chown root:root /app-entrypoint.sh
RUN chown root:root /apache-init.sh
RUN chown root:root /post-init.sh
RUN chown root:root /tfc-init.sh
RUN chown root:root /tfc-install.sh
RUN chown root:root /database-init.sh
RUN chmod a+x /app-entrypoint.sh
RUN chmod a+x /apache-init.sh
RUN chmod a+x /post-init.sh
RUN chmod a+x /tfc-init.sh
RUN chmod a+x /tfc-install.sh
RUN chmod a+x /database-init.sh

EXPOSE 80 443

ENTRYPOINT [ "/app-entrypoint.sh" ]
CMD [ "nami", "start", "--foreground", "apache" ]