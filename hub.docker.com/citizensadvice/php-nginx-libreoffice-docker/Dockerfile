FROM centos:7

ENV NODEJS_DOWNLOAD_SHA256 159e5485d0fb5c913201baae49f68fd428a7e3b08262e9bf5003c1b399705ca8

RUN rpm -Uvh http://www.city-fan.org/ftp/contrib/yum-repo/city-fan.org-release-2-1.rhel7.noarch.rpm && \
    yum install -y epel-release deltarpm  wget inetutils-ping && \
    yum-config-manager --enable city-fan.org && \
    yum update -y && \
    yum install -y curl libcurl python-pip gcc-c++ git make patch \
    freetds unixODBC unixODBC-devel libtool-ltdl libtool-ltdl-devel \
    ruby ruby-devel ruby-libs mysql zip unzip bind-utils nmap dnsmasq && \
    yum install -y libreoffice vim mailx sendmail && \
    yum clean -y all && rm -rf /var/cache/yum

ARG PHP_VERSION=5.6
ARG ZS_INSTALL_ARGS="nginx --automatic"

ADD ZendServer-RepositoryInstaller-linux /ZendServer-RepositoryInstaller-linux

RUN chmod 775 /ZendServer-RepositoryInstaller-linux/*.sh
RUN chmod 775 /ZendServer-RepositoryInstaller-linux/nginx/*.sh
RUN rpm --import http://repos.zend.com/zend.key \
  && /ZendServer-RepositoryInstaller-linux/install_zs.sh ${PHP_VERSION} ${ZS_INSTALL_ARGS} && \
  chown -R zend: /usr/local/zend

RUN mkdir /etc/dhcp/ && \
    echo 'prepend domain-name-servers 127.0.0.1;' >> /etc/dhcp/dhclient.conf && \
    ln -s /usr/local/zend/bin/php /usr/bin/php && \
    ln -s /usr/local/zend/bin/php-fpm /usr/bin/php-fpm && \
    ln -s /usr/local/zend/bin/php-config /usr/bin/php-config && \
    ln -s /usr/bin/ruby /usr/share/ruby


RUN pip install pyentrypoint && sed -i -e "/self._rm_dockerenv()/d" /lib/python2.7/site-packages/pyentrypoint/command.py

RUN wget https://nodejs.org/download/release/v0.10.33/node-v0.10.33-linux-x64.tar.gz && \
    echo "$NODEJS_DOWNLOAD_SHA256 node-v0.10.33-linux-x64.tar.gz" | sha256sum -c - && \
    tar --strip-components 1 -xzvf node-v* -C /usr/local && \
    npm -gf install grunt && \
    npm -gf install grunt-cli && \
    rm -f node-v0.10.33-linux-x64.tar.gz

RUN pip install awscli --upgrade --user

# install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    # enable parallel install
    composer global require hirak/prestissimo

