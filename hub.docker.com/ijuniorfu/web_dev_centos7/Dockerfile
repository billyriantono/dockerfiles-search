
# 基础镜像
FROM ijuniorfu/centos7-systemd

# 维护者信息
MAINTAINER ijuniorfu@gmail.com

# 镜像操作命令
RUN yum clean all && \
yum makecache && \
yum update -y && \
rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm && \
yum -y install ntp make openssl openssl-devel pcre pcre-devel libpng libpng-devel libjpeg-6b libjpeg-devel-6b freetype freetype-devel gd gd-devel zlib zlib-devel gcc gcc-c++ libXpm libXpm-devel ncurses ncurses-devel libmcrypt libmcrypt-devel libxml2 gcc gcc-c++ libXpm libXpm-devel ncurses ncurses-devel libmcrypt libmcrypt-devel libxml2 && \
yum install -y nginx && \
yum -y install php72w php72w-pdo php72w-soap php72w-opcache php72w-mcrypt php72w-mbstring php72w-gd php72w-fpm php72w-cli php72w-mysqlnd php72w-pear php72w-pecl-imagick php72w-pecl-imagick-devel php72w-pecl-redis php72w-pecl-mongodb php72w-pecl-memcached php72w-pecl-xdebug php72w-imap php72w-devel php72w-bcmath php72w-pecl-apcu php72w-pecl-apcu-devel php72w-pecl-igbinary && \
sed -i -e 's/user = apache/user = root/' /etc/php-fpm.d/www.conf && \
sed -i -e 's/group = apache/group = root/' /etc/php-fpm.d/www.conf

RUN  yum -y install kde-l10n-Chinese && \
yum -y reinstall glibc-common && \
localedef -c -f UTF-8 -i zh_CN zh_CN.utf8 && \
echo "export LANG=zh_CN.UTF-8" >> /etc/profile && \
echo "export LC_ALL=zh_CN.UTF-8" >> /etc/profile && \
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
yum -y install git && \
yum -y install wget && \
yum -y install tar && \
yum -y install telnet && \
yum -y install net-tools && \
yum -y install crontabs && \
systemctl enable crond.service && \
systemctl enable php-fpm.service&& \
systemctl enable nginx.service && \
sed -i -e 's/php-fpm --nodaemonize/php-fpm -R --daemonize/' /usr/lib/systemd/system/php-fpm.service

ENV LANG zh_CN.UTF-8
ENV LC_ALL zh_CN.UTF-8

# composer安装
RUN  curl -s http://getcomposer.org/installer | php && \
mv composer.phar /usr/bin/composer

ENV ROOT_PASSWORD 123456

# ssh安装
RUN yum install openssh-server -y && \
echo $ROOT_PASSWORD | passwd root --stdin && \
systemctl enable sshd.service && \
rm -rf /tmp/*

WORKDIR /

# centos7 容器启动命令
CMD ["/usr/sbin/init"]
