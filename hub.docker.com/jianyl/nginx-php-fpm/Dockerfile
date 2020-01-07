FROM richarvey/nginx-php-fpm:1.5.7
MAINTAINER ljy "sal597685816@live.cn"

ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
  && apk add gcc g++ m4 autoconf make readline readline-dev && wget https://ftp.postgresql.org/pub/source/v10.3/postgresql-10.3.tar.gz \
  && tar xzf postgresql-10.3.tar.gz \
  && cd postgresql-10.3 && ./configure && make && make install && /usr/local/bin/docker-php-ext-configure pgsql \
  && /usr/local/bin/docker-php-ext-install pgsql bcmath && /usr/local/bin/docker-php-ext-configure pdo_pgsql && \
  /usr/local/bin/docker-php-ext-install pdo_pgsql && no | pecl install redis && echo "extension=redis.so" > /usr/local/etc/php/conf.d/pecl-redis.ini \
  && pecl install mongodb && echo "extension=mongodb.so" > /usr/local/etc/php/conf.d/pecl-mongodb.ini && pecl install grpc \
  && echo "extension=grpc.so" > /usr/local/etc/php/conf.d/pecl-grpc.ini && pecl install protobuf \
  && echo "extension=protobuf.so" > /usr/local/etc/php/conf.d/pecl-protobuf.ini && rm -rf /tmp/pear/download/* \
  && supervisorctl restart php-fpm && wget https://github.com/tideways/php-xhprof-extension/archive/v4.1.6.tar.gz -O /tmp/xhprof.tar.gz \
  && cd /tmp \
  && tar -xzvf xhprof.tar.gz \
  && cd /tmp/php-xhprof-extension-4.1.6 \
  && phpize \
  && ./configure \
  && make \
  && make install \
  && cd - \
  && rm /tmp/xhprof.tar.gz \
  && rm -rf /tmp/php-xhprof-extension-4.1.6 \
  && echo -e "extension=tideways.so\ntideways.auto_prepend_library=0\ntideways.sample_rate=100" > /usr/local/etc/php/conf.d/tideways.ini \ 
  && apk del gcc g++ m4 autoconf make readline readline-dev && rm -rf /var/www/html/* \
  && cd /usr/local && wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-4.0.5.tgz \
  && tar -xzf mongodb-linux-x86_64-4.0.5.tgz -C /usr/local && mv /usr/local/mongodb-linux-x86_64-4.0.5 /usr/local/mongodb \
  && export PATH=/usr/local/mongodb/bin:$PATH && source /etc/profile && rm -rf mongodb-linux-x86_64-4.0.5.tgz \
  && echo "date.timezone=PRC" > /usr/local/etc/php/conf.d/date-timezone.ini && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
