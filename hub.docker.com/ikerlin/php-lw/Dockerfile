FROM php:7.1-fpm-alpine

# 删除国外地址
# RUN  echo > /etc/apk/repositories

# Install env 添加国内镜像到顶部
#RUN sed -i '1i\http://mirrors.ustc.edu.cn/alpine/v3.4/main/' /etc/apk/repositories
#RUN sed -i '1i\http://mirrors.ustc.edu.cn/alpine/v3.4/community/' /etc/apk/repositories
#RUN sed -i '1i\http://mirrors.aliyun.com/alpine/v3.4/main/' /etc/apk/repositories
#RUN sed -i '1i\http://mirrors.aliyun.com/alpine/v3.4/community/' /etc/apk/repositories


#更新软件和必要库
RUN apk update --no-cache && \
#    apk upgrade --no-cache && \
    apk add --no-cache \
        freetype \
        libmcrypt \
        libjpeg-turbo \
        libpng \
        openssl \
        hiredis \
        hiredis-dev \
        libmcrypt-dev \
        freetype-dev \
        openssl-dev \
        libjpeg-turbo-dev \
        libpng-dev \
        bash ca-certificates tzdata \
        linux-headers \
        musl \
        gcc \
        libtool 

#分配Hugepages(设置在宿主机上设置即可)
# RUN sysctl  vm.nr_hugepages=128

#安装扩展
RUN  docker-php-ext-install  gd zip mcrypt mbstring pdo_mysql opcache pcntl
 

#php扩展编译需要
RUN apk add --no-cache --virtual .phpize-deps $PHPIZE_DEPS 


# Install PHP extensions phalcon

#RUN echo "memory_limit = 256M;" >> /usr/local/etc/php/php.ini

RUN curl -O  https://codeload.github.com/phalcon/cphalcon/tar.gz/v3.1.2
RUN tar xvzf v3.1.2
RUN cd cphalcon-3.1.2/build && ./install
RUN cd ../../ && rm -Rf cphalcon-3.1.2 && rm -Rf v3.1.2
RUN echo "extension=phalcon.so" > /usr/local/etc/php/conf.d/phalcon.ini 


# Install PHP extensions swoole
RUN  pecl install swoole-1.9.11 
RUN  echo -e "extension=swoole.so\nswoole.use_namespace=On" > /usr/local/etc/php/conf.d/swoole.ini 

# Install PHP extensions phpredis
RUN  pecl install redis-3.1.2 
RUN  echo "extension=redis.so" > /usr/local/etc/php/conf.d/phpredis.ini 

# Install PHP extensions yac
RUN  pecl install yac-2.0.1 
RUN  echo -e "extension=yac.so\nyac.enable_cli = 1" > /usr/local/etc/php/conf.d/yac.ini 
# Install PHP protobuf
#RUN  pecl install protobuf-3.1

#core dump test
#RUN echo '/tmp/core.%p' > /proc/sys/kernel/core_pattern
#RUN apt-get install -y gdb

#安装debug扩展
RUN  pecl install xdebug-2.5.0 
RUN  echo "zend_extension=xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini 

#删除文件包
#RUN apk cache clean 
RUN apk del .phpize-deps
#清理缓存
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/* /var/cache/apk/
#RUN rm -rf /var/cache/apk/* && rm -rf /var/lib/apt/lists/*
# delete pecl install tmp
#RUN  rm -r /tmp/pear
#RUN  rm -r /var/tmp

# PHP config
RUN ln -sf /opt/config/php.ini    /usr/local/etc/php/php.ini
RUN ln -sf /opt/config/php-fpm.conf    /usr/local/etc/php-fpm.conf

#设置时区
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" > /etc/timezone


# Composer
ADD composer.phar /usr/local/bin/composer
RUN chmod 755 /usr/local/bin/composer

WORKDIR /data


EXPOSE 9000
