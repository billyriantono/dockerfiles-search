# Version: 0.0.1
FROM centos:7.4.1708
MAINTAINER jxie "506512796@qq.com"
ENV REFRESHED_AT 2019-12-25
RUN yum -y update && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    yum install httpd-2.4.6-90.el7.centos.x86_64 httpd-devel-2.4.6-90.el7.centos.x86_64 -y && \
    yum install epel-release -y && rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm && \
    yum install php72w php72w-pear php72w-cli php72w-fpm php72w-mbstring php72w-pdo php72w-mcrypt php72w-xml php72w-mysqlnd \
    php72w-gd php72w-devel php72w-pecl-xdebug php72w-intl php72w-xmlrpc php72w-soap php72w-opcache php72w-pecl-redis -y && \
    yum install -y hiredis libtool make gcc gcc-c++ && curl -O http://pecl.php.net/get/swoole-4.3.5.tgz && \
    tar -zxf swoole-4.3.5.tgz && cd swoole-4.3.5 && phpize && ./configure --with-php-config=/usr/bin/php-config && make && make install && \
    echo -e "; Enable redis extension module\nextension=swoole.so" > /etc/php.d/swoole.ini && cd ../ && rm -rf ./swoole-4.3.5.tgz swoole-4.3.5 && \
    sed -i '/IncludeOptional conf.d\/\*.conf/i\\nInclude conf.d\/vhost\/\*.conf\n' /etc/httpd/conf/httpd.conf && \
    sed -ie 's/#ServerName www.example.com:80/ServerName localhost:80/' /etc/httpd/conf/httpd.conf && \
    sed -ie 's/display_errors = Off/display_errors = On/' /etc/php.ini && \
    sed -i '$a\\nxdebug.remote_enable=1\nxdebug.remote_host=host.docker.internal\nxdebug.remote_port=9012\nxdebug.idekey=PHPSTORM' /etc/php.d/xdebug.ini
CMD ["/usr/sbin/httpd", "-DFOREGROUND"]
EXPOSE 80 8080