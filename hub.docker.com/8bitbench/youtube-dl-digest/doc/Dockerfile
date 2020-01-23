FROM php:7.4.1-fpm-alpine3.10

#分配Hugepages(设置在宿主机上设置即可)
# RUN sysctl  vm.nr_hugepages=128

#RUN echo "memory_limit = 256M;" >> /usr/local/etc/php/php.ini
ENV LANG=C.UTF-8
#更新软件和必要库
#php扩展编译需要
#安装扩展
#Install PHP extensions phpredis
ENV REDIS_VERSION=5.1.1
#Install PHP protobuf
ENV PROTOBUF_VERSION=3.11.2
#Install PHP extensions swoole
ENV SWOOLE_VERSION=4.4.13
#Install PHP extensions phalcon
ENV PHALCON_VERSION=4.0.0
ENV PSR_VERSION=0.7.0
#安装debug扩展
ENV XDEBUG_VERSION=2.9.0
#安装inotify扩展
ENV INOTIFY_VERSION=2.0.0
#安装yaml扩展
ENV YAML_VERSION=2.0.4
# xdebug apk add py-pygraphviz python
# 删除国外地址 Install env 添加国内镜像到顶部
# RUN  echo > /etc/apk/repositories \
# && sed -i '1i\http://mirrors.ustc.edu.cn/alpine/v3.9/main/' /etc/apk/repositories \
# && sed -i '1i\http://mirrors.ustc.edu.cn/alpine/v3.9/community/' /etc/apk/repositories \
# && sed -i '1i\http://mirrors.aliyun.com/alpine/v3.9/main/' /etc/apk/repositories \
# && sed -i '1i\http://mirrors.aliyun.com/alpine/v3.9/community/' /etc/apk/repositories \
RUN  apk update --no-cache  \
  && apk add --no-cache vim jq gmp-dev libpng-dev libzip-dev  openssl-dev openssh-client yaml-dev gzip \
     protobuf-dev linux-headers bash $PHPIZE_DEPS  libbsd  bash bash-doc bash-completion \
  && docker-php-ext-configure gmp \
  && docker-php-ext-configure gd \
  && docker-php-ext-install gmp sockets gd zip  pdo_mysql opcache pcntl \
  && pecl install yaml-${YAML_VERSION} && docker-php-ext-enable yaml \
  && echo "install yaml ok !" \
  && pecl install redis-${REDIS_VERSION} && docker-php-ext-enable redis \
  && echo "install redis ok !" \
  && pecl install protobuf-${PROTOBUF_VERSION} && docker-php-ext-enable protobuf \
  && echo "install protobuf ok !" \
  && printf "yes\n yes\n yes\n yes\n" |  pecl install  swoole-${SWOOLE_VERSION} \
  && docker-php-ext-enable swoole \
  && echo "install swoole ok !" \
  && pecl install psr-${PSR_VERSION} && docker-php-ext-enable psr \
  && echo "install psr ok !" \
  && curl -s -L https://codeload.github.com/phalcon/cphalcon/tar.gz/v${PHALCON_VERSION} | tar -xvzf - -C /tmp \
  && cd /tmp/cphalcon-${PHALCON_VERSION}/build && ./install \
  && echo -e "extension = phalcon.so;\nphalcon.orm.exception_on_failed_save = On;\nphalcon.orm.column_renaming = Off;\nphalcon.orm.not_null_validations = Off;" > /usr/local/etc/php/conf.d/phalcon.ini  \
  && cd /tmp && rm -r /tmp/cphalcon-${PHALCON_VERSION} \
  && echo "install cphalcon ok !" \
  && pecl install inotify-${INOTIFY_VERSION} \
  && echo "install inotify ok !" \
  && pecl install xdebug-${XDEBUG_VERSION}  \
  && echo "install xdebug ok !" \
  && curl -L https://github.com/composer/composer/releases/download/1.8.5/composer.phar  -o /usr/local/bin/composer \
  && chmod +x /usr/local/bin/composer \
  && echo -e "disable_functions = phpinfo,eval,passthru,exec,system,chroot,chgrp,chown,shell_exec,proc_open,proc_get_status,ini_alter,ini_alter,ini_restore,dl,pfsockopen,readlink,symlink,popepassthru,stream_socket_server,fsocket,fsockopen;\nexpose_php = Off;" > /usr/local/etc/php/conf.d/safety.ini  \
  && apk del bash $PHPIZE_DEPS \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/apk/* \
           /usr/share/doc/* /name/usr/share/man/* /usr/share/info/* \
  && sed -i 's#root:x:0:0:root:/root:/bin/ash#root:x:0:0:root:/root:/bin/bash#g' /etc/passwd


#卸载phpize-deps
#清理缓存
#core dump test
#RUN echo '/tmp/core.%p' > /proc/sys/kernel/core_pattern
#RUN apt-get install -y gdb
WORKDIR /data/www
