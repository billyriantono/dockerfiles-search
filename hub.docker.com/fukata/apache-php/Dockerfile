FROM centos:7.6.1810

RUN yum update -y \
    && yum upgrade -y \
    && yum install -y wget \
                      httpd \
                      mod_ssl \
    && yum install -y epel-release \
    && yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm \
    && yum install -y yum-utils \
    && yum-config-manager --disable remi-php54 \
    && yum-config-manager --enable remi-php73 \
    && yum update -y \
    && yum install -y php \
                      php-fpm \
                      php-dom \
                      php-gd \
                      php-mbstring \
                      php-mcrypt \
                      php-mysqlnd \
                      php-mysqli \
                      php-pdo \
                      php-sqlite \
                      php-pecl-redis \
                      php-wddx \
                      php-xml \
                      php-xsl \
                      php-mcrypt* \
    && useradd -u 1000 -U -M www-data

WORKDIR /etc/httpd

EXPOSE 80 443
CMD ["httpd", "-DFOREGROUND", "-d", "/etc/httpd"]
