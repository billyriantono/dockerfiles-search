### Build msmtp rpm package
FROM    bigcatmm/docker-base-images:rpm-builder-latest AS msmtp-rpm-build
WORKDIR rpmbuild

COPY    build_specs/msmtp-1.8.3.spec SPECS/
RUN     spectool -R -g SPECS/msmtp-1.8.3.spec && \
        rpmbuild -bb --clean SPECS/msmtp-1.8.3.spec      

### Release msmtp rpm package
FROM    scratch AS msmtp-1.8.3-1-rpm
WORKDIR /
COPY    --from=msmtp-rpm-build /root/rpmbuild/RPMS/x86_64/msmtp-1.8.3-1.el6.x86_64.rpm .

### Test msmtp rpm package
FROM    bigcatmm/docker-base-images:server-latest AS test-msmtp-rpm
COPY    --from=msmtp-1.8.3-1-rpm /msmtp-1.8.3-1.el6.x86_64.rpm /tmp/
RUN     yum install -y /tmp/msmtp-1.8.3-1.el6.x86_64.rpm

CMD         ["--version"]
ENTRYPOINT  ["msmtp"]

###############################################################################

###
### PHP Service Base Stage
###

FROM    bigcatmm/docker-base-images:server-latest AS php-service-base

ARG     TIMEZONE
ARG     BUILD_DATE
ARG     SOURCE_REPOSITORY_URL
ARG     SOURCE_COMMIT

LABEL   org.opencontainers.image.title="PHP-Service-Base" \
        org.opencontainers.image.description="A base CENTOS 6 image with PHP 5.3.29 and minimal configuration." \
        org.opencontainers.image.created=$BUILD_DATE \
        org.opencontainers.image.source=$SOURCE_REPOSITORY_URL \
        org.opencontainers.image.revision=$SOURCE_COMMIT

# Use IUS Repo
# NOTE: php53u* packages install from the IUS-archive
RUN     yum -y install https://centos6.iuscommunity.org/ius-release.rpm && \
        rpm --import /etc/pki/rpm-gpg/IUS-COMMUNITY-GPG-KEY

# Install packages
RUN     PHP_PKGS="php53u \
                  php53u-bcmath \
                  php53u-cli \
                  php53u-common \
                  php53u-dba \
                  php53u-fpm \
                  php53u-mbstring \
                  php53u-mcrypt \
                  php53u-mysql \
                  php53u-pdo \
                  php53u-pear \
                  php53u-process \
                  php53u-suhosin \
                  php53u-xcache \
                  php53u-xml" && \
        yum -y update && \
        yum install -y git unzip && \
        yum --enablerepo=ius-archive install -y ${PHP_PKGS} && \
        yum clean all

# Rename the apache user/group to a more generic www-data
RUN set -ex ; \
        groupmod -n www-data apache ; \
        usermod -l www-data -c "Web server" apache
 
# Set System Timezone
RUN set -ex ; \
        sed -e "s~^\(TIMEZONE=\).*$~\1${TIMEZONE:-UTC}~" \
            -i /etc/sysconfig/clock ; \
        ln -snf /usr/share/zoneinfo/${TIMEZONE:-UTC} /etc/localtime ; \
        echo ${TIMEZONE:-UTC} > /etc/timezone ; \
        sed -r -e "s~^;?(date.timezone[ ]+=).*$~\1 ${TIMEZONE:-UTC}~" \
            -i /etc/php.ini

# Install Composer
RUN set -ex ; \
        sed -re "s~^;?(suhosin.executor.include.whitelist[ ]+=).*$~\1 phar~" \
            -i /etc/php.d/suhosin.ini ; \
        curl -sS https://getcomposer.org/installer | \
        php -d allow_url_fopen=on -- --install-dir=/usr/local/bin --filename=composer



###
### PHP-FPM Service Stage
###

FROM    php-service-base AS php-fpm

ARG     BUILD_DATE
ARG     SOURCE_REPOSITORY_URL
ARG     SOURCE_COMMIT

LABEL   org.opencontainers.image.title="PHP-FPM-Service" \
        org.opencontainers.image.description="A base CENTOS 6 image with PHP 5.3.29 and php-fpm configured to listen on localhost:9000." \
        org.opencontainers.image.created=$BUILD_DATE \
        org.opencontainers.image.source=$SOURCE_REPOSITORY_URL \
        org.opencontainers.image.revision=$SOURCE_COMMIT

# Enable short tags 
RUN     sed -e '/^short_open_tag /s/= Off/= On/' \
            -i /etc/php.ini

# Update config for php-fpm
RUN     sed -e 's/127.0.0.1:9000/9000/' \
            -e '/allowed_clients/d' \
            -e '/catch_workers_output/s/^;//' \
        	-e '/status_path/s/^;//' \
            -e '/error_log/d' \
	        -e 's/user = apache/user = www-data/' \
	        -e 's/group = apache/group = www-data/' \
            -i /etc/php-fpm.d/www.conf

# Ensure that the source dir exists
RUN     mkdir -p /var/www
VOLUME  ["/var/www"]

# Expose port 9000 for php-fpm requests
EXPOSE  9000

CMD         ["--nodaemonize"]
ENTRYPOINT  ["/usr/sbin/php-fpm"]



###
### Add msmtp to the php base image
###

FROM    php-fpm AS php-fpm-msmtp

ARG     BUILD_DATE
ARG     SOURCE_REPOSITORY_URL
ARG     SOURCE_COMMIT

LABEL   org.opencontainers.image.title="PHP-FPM-msmtp-Service" \
        org.opencontainers.image.description="Based on the PHP-FPM-Service image with PHP 5.3.29, and configured to relay mail via msmtp." \
        org.opencontainers.image.created=$BUILD_DATE \
        org.opencontainers.image.source=$SOURCE_REPOSITORY_URL \
        org.opencontainers.image.revision=$SOURCE_COMMIT

# Install compiled msmtp files
COPY    --from=msmtp-1.8.3-1-rpm /msmtp-1.8.3-1.el6.x86_64.rpm /tmp/
RUN     yum install -y /tmp/msmtp-1.8.3-1.el6.x86_64.rpm && \
        rm -f /tmp/msmtp-1.8.3-1.el6.x86_64.rpm

# Write config for msmtp gmail account
COPY    msmtprc /etc/msmtprc
RUN     chown www-data:www-data /etc/msmtprc && \
        chmod 600 /etc/msmtprc

# Use msmtp to send mail in PHP
COPY    mail.ini /etc/php.d/mail.ini

