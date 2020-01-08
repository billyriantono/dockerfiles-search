FROM centos:6
MAINTAINER tnaototo

USER root
WORKDIR /root

# Install modules
RUN yum -y update
RUN yum -y install http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el6.rf.x86_64.rpm
RUN rpm -Uvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
RUN yum -y update --enablerepo=rpmforge,epel,remi,remi-php55

RUN yum -y install passwd openssh openssh-clients openssh-server httpd vim python-setuptools git sudo

RUN yum -y install --enablerepo=remi,remi-php55 php php-opcache php-devel php-mbstring php-mcrypt php-mysql php-phpunit-PHPUnit php-pecl-xdebug php-cli php-common


# Apache設定
COPY config/httpd.conf /etc/httpd/conf/httpd.conf


# PHP設定
COPY config/php.ini /etc/php.ini


# supervisordのインストール
RUN easy_install supervisor

# supervisordの設定
RUN echo_supervisord_conf > /etc/supervisord.conf
RUN echo '[include]' >> /etc/supervisord.conf
RUN echo 'files = supervisord/conf/*.conf' >> /etc/supervisord.conf
RUN mkdir -p /etc/supervisord/conf/
COPY config/supervisor.conf /etc/supervisord/conf/service.conf


# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin


# ポート開放
EXPOSE 80


# 起動時にsupervisordを実行
CMD ["/usr/bin/supervisord"]
