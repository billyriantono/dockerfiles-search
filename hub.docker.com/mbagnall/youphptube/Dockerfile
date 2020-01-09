FROM centos:7

# Set our our meta data for this container.
LABEL name="YouPHPTube Server Container"
LABEL description="A Docker Container for the YouPHPTube software project."
LABEL author="Michael R. Bagnall <mrbagnall@icloud.com>"
LABEL vendor="FlyingFlip Studios"
LABEL version="1.1"

# Set up our standard binary paths.
ENV PATH /usr/local/src/vendor/bin/:/usr/local/rvm/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# Set TERM env to avoid mysql client error message "TERM environment variable not set" when running from inside the container
ENV TERM xterm

# Fix command line compile issue with bundler.
ENV LC_ALL en_US.utf8

# Install and enable repositories
RUN yum -y update
RUN yum -y install epel-release && \
  yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
  rpm -Uvh https://centos7.iuscommunity.org/ius-release.rpm && \
  rpm --import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro && \
  rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-1.el7.nux.noarch.rpm && \
  yum -y update && \
  yum -y install yum-utils && \
  curl -sL https://rpm.nodesource.com/setup_10.x | bash -

RUN yum -y groupinstall "Development Tools" && \
  yum -y install \
  git \
  mariadb \
  wget \
  which \
  gd-devel.x86_64 \
  perl-App-cpanminus.noarch \
  cronie.x86_64 \
  mod_ssl.x86_64 \
  gettext \
  docker \
  bzip2 \
  gcc \
  gcc-c++ \
  make \
  nodejs \
  logrotate \
  webalizer \
  ffmpeg \
  ffmpeg-devel \
  perl-Image-ExifTool

# Install PHP modules
RUN yum-config-manager --enable remi-php72
RUN yum -y install \
  php \
  php-bcmath \
  php-curl \
  php-gd \
  php-imap \
  php-mbstring \
  php-mysqlnd \
  php-pgsql \
  php-odbc \
  php-pear \
  php-pecl-imagick \
  php-opcache \
  php-pecl-memcached \
  php-xml \
  php-pecl-redis \
  php-pecl-ssh2 \
  php-ldap
RUN yum -y install php72-php-pecl-mcrypt.x86_64

# Perform yum cleanup
RUN yum -y upgrade && \
    yum clean all

RUN rm -rf /var/www/html
RUN mkdir -p /var/www/html && \
  cd /var/www/html && \
  git clone https://github.com/YouPHPTube/YouPHPTube.git streamer && \
  chown -R apache:apache /var/www/html

USER root

COPY etc/httpd/conf/httpd-auth.conf /etc/httpd/conf/httpd-auth.conf
COPY etc/httpd/conf/httpd-noauth.conf /etc/httpd/conf/httpd-noauth.conf
COPY etc/php.ini /etc/php.ini

ADD conf/run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh
RUN chown apache:apache /run-httpd.sh

VOLUME ["/var/www"]

EXPOSE 80 443

CMD ["/run-httpd.sh"]