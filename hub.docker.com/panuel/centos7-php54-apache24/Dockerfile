FROM panuel/centos7-php54-apache24:latest 

RUN yum -y update --disableplugin=fastestmirror && \
    yum -y --disableplugin=fastestmirror --setopt=tsflags=nodocs install \
      php-pear \
      php-devel \
      gcc \
      gcc-c++ \
      autoconf \
      automake \
      make \
      wget \ 
      && \
    pecl channel-update pecl.php.net && \
    pecl install xdebug-2.4.1 && \
    yum -y remove make gcc gcc-c++ autoconf automake php-pear php-devel wget && \
    package-cleanup -q --leaves | xargs -l1 yum -y remove  && \
    yum -y  --disableplugin=fastestmirror --setopt=tsflags=nodocs install openssl && \
    yum clean all && \
    rm -rf /var/cache/yum 
 
RUN mkdir /xdebug && chmod 777 /xdebug

ADD xdebug.ini /etc/php.d/
