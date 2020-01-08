FROM centos:7

MAINTAINER Andreas Kleiber <andreas.kleiber@8select.de>

# set some variables to easily update appserver.io version
ENV APPSERVER_VERSION 1.1.0
ENV APPSERVER_RUNTIME_BUILD_VERSION 1.1.0-26
ENV APPSERVER_RUNTIME_FILE_PATH /tmp/appserver-runtime.rpm
ENV APPSERVER_SOURCE_VERSION 1.1.0

# add repos for appserver.io dependencies
RUN yum install -y epel-release wget \
    && wget -O /tmp/remi.rpm \
        http://rpms.famillecollet.com/enterprise/remi-release-7.rpm \
    && rpm -i /tmp/remi.rpm \

    # install appserver.io runtime and dependencies
    && wget -O ${APPSERVER_RUNTIME_FILE_PATH} \
        https://github.com/appserver-io/appserver/releases/download/${APPSERVER_VERSION}/appserver-runtime-${APPSERVER_RUNTIME_BUILD_VERSION}.el7.centos.x86_64.rpm \
    && yum --nogpgcheck localinstall -y ${APPSERVER_RUNTIME_FILE_PATH} \
    && rm -f ${APPSERVER_RUNTIME_FILE_PATH} \

    # make appserver.io php always available
    && ln -s /opt/appserver/bin/php /usr/local/bin/php \

    # install composer
    && php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /root

# install appserver.io dist
# download appserver source in specific version
RUN wget https://github.com/appserver-io/appserver/archive/${APPSERVER_SOURCE_VERSION}.tar.gz \

    # extract appserversource
    && tar -xzf ${APPSERVER_SOURCE_VERSION}.tar.gz \
    && cd appserver-${APPSERVER_SOURCE_VERSION} \

    # install dependencies using composer, use --prefer-source to avoid github rate limit
    && composer install --no-dev --no-interaction --prefer-source \

    # modify user-rights in configuration
    && sed -i "s/www-data/root/g" etc/appserver/appserver.xml \

    # copy appserver source using ant integration
    && cp -r * /opt/appserver/ \

    # remove appserver source
    && rm -f /root/${APPSERVER_SOURCE_VERSION}.tar.gz \
    && rm -rf /root/appserver-${APPSERVER_SOURCE_VERSION} \

    # install supervisor, the system that makes sure appserver processes are running
    && yum install -y supervisor \
    && mkdir -p /var/log/supervisor \

    # cleanup yum to free space
    && yum clean all

# let php log to stderr
RUN ln -sf /dev/stderr /opt/appserver/var/log/php_errors.log \
    && ln -sf /dev/stderr /opt/appserver/var/log/php-fpm.log

# copy configuration files
COPY conf/supervisord.conf /etc/
COPY conf/appserver.xml /opt/appserver/etc/appserver/

# expose ports
EXPOSE 9080 9443

# run supervisord
CMD []
ENTRYPOINT ["/usr/bin/supervisord"]
