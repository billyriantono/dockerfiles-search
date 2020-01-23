FROM centos:centos7
LABEL maintainer="Shrinivas Ambat <ambatshri@gmail.com>" 
RUN rpm -Uhv https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
    rpm -Uhv http://rpms.famillecollet.com/enterprise/remi-release-7.rpm  && \
    yum -y --setopt=tsflags=nodocs install yum-utils && \
    yum-config-manager --enable remi-php56 && \
    yum -y --setopt=tsflags=nodocs install php php-mcrypt php-cli php-gd php-curl php-soap \
    php-mysql php-ldap php-zip php-fileinfo php-imap php-opcache php-xmlrpc php-mbstring php-simplexml php-apcu vim openssh-7.4p1-21.el7.x86_64 openssl && \
    sed -i "s/memory_limit = 128M/memory_limit = 256M/" /etc/php.ini && \
    sed -i "s/;date.timezone =/date.timezone = Asia\/Kolkata/" /etc/php.ini && \
    yum clean all
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
EXPOSE 80