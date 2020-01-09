FROM centos/s2i-base-centos7

# This image provides an Apache+PHP environment for running PHP
# applications.

EXPOSE 8080

ENV PHP_VERSION=7.2 \
    PATH=$PATH:/opt/remi/php72/root/usr/bin \
    LANG=en_AU.UTF-8 \
    LC_ALL=en_AU.UTF-8

ENV SUMMARY="Platform for building and running PHP $PHP_VERSION applications" \
    DESCRIPTION="PHP $PHP_VERSION available as docker container is a base platform for \
building and running various PHP $PHP_VERSION applications and frameworks. \
PHP is an HTML-embedded scripting language. PHP attempts to make it easy for developers \
to write dynamically generated web pages. PHP also offers built-in database integration \
for several commercial and non-commercial database management systems, so writing \
a database-enabled webpage with PHP is fairly simple. The most common use of PHP coding \
is probably as a replacement for CGI scripts."

LABEL summary="$SUMMARY" \
      description="$DESCRIPTION" \
      io.k8s.description="$DESCRIPTION" \
      io.k8s.display-name="Apache 2.4 with PHP 7.2" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,php,php72,rh-php72" \
      name="centos/php-72-centos7" \
      com.redhat.component="rh-php72-docker" \
      version="1" \
      maintainer="SoftwareCollections.org <sclorg@redhat.com>"

# Install Apache httpd and PHP
RUN wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm -O /tmp/epel-release-latest-7.noarch.rpm && \
    wget http://rpms.remirepo.net/enterprise/remi-release-7.rpm -O /tmp/remi-release-7.rpm && \
    rpm -Uvh /tmp/remi-release-7.rpm /tmp/epel-release-latest-7.noarch.rpm && \
    yum install -y centos-release-scl && \
    yum-config-manager --enable centos-sclo-rh-testing && \
    INSTALL_PKGS="httpd24-httpd php72 php72-php php72-php-mysqlnd php72-php-pgsql php72-php-bcmath \
                  php72-php-gd php72-php-intl php72-php-ldap php72-php-mbstring php72-php-pdo \
                  php72-php-process php72-php-soap php72-php-opcache php72-php-xml php72-php-pecl-libsodium \
                  php72-php-gmp php72-php-pecl-apcu rh-mariadb102-mariadb rh-postgresql96 \
                  php72-php-pecl-redis php72-php-ast" && \
    yum install -y --setopt=tsflags=nodocs $INSTALL_PKGS --nogpgcheck && \
    rpm -V $INSTALL_PKGS && \
    mv /etc/httpd/conf.d/php72-php.conf /opt/rh/httpd24/root/etc/httpd/conf.d/ && \
    mv /etc/httpd/conf.modules.d/15-php72-php.conf /opt/rh/httpd24/root/etc/httpd/conf.modules.d/ && \
    mv /etc/httpd/modules/libphp72.so /opt/rh/httpd24/root/etc/httpd/modules/ && \
    rpm -ev --nodeps $(rpm -qa httpd) && \
    rpm -ev --nodeps $(rpm -qa httpd-tools) && \
    yum clean all -y && \
    rm -rf /var/cache/yum && \
    rm /tmp/epel-release-latest-7.noarch.rpm /tmp/remi-release-7.rpm

# Copy the S2I scripts from the specific language image to $STI_SCRIPTS_PATH
COPY ./s2i/bin/ $STI_SCRIPTS_PATH

# Copy extra files to the image.
COPY ./root/ /

# In order to drop the root user, we have to make some directories world
# writeable as OpenShift default security model is to run the container under
# random UID.
RUN sed -i -f ${APP_ROOT}/etc/httpdconf.sed /opt/rh/httpd24/root/etc/httpd/conf/httpd.conf && \
    sed -i '/php_value session.save_path/d' /opt/rh/httpd24/root/etc/httpd/conf.d/php72-php.conf && \
    head -n151 /opt/rh/httpd24/root/etc/httpd/conf/httpd.conf | tail -n1 | grep "AllowOverride All" || exit && \
    echo "IncludeOptional ${APP_ROOT}/etc/conf.d/*.conf" >> /opt/rh/httpd24/root/etc/httpd/conf/httpd.conf && \
    mkdir /tmp/sessions && \
    mkdir /tmp/opcache && \
    chown -R 1001:0 ${APP_ROOT} /tmp/sessions /tmp/opcache && \
    chmod -R a+rwx /tmp/sessions && \
    chmod -R a+rwx /tmp/opcache && \
    chmod -R ug+rwx ${APP_ROOT} && \
    chmod -R a+rwx /etc/opt/remi/php72 && \
    chmod -R a+rwx /opt/rh/httpd24/root/var/run/httpd && \
    rpm-file-permissions

USER 1001

# Set the default CMD to print the usage of the language image
CMD $STI_SCRIPTS_PATH/usage
