FROM ubuntu:16.04
ENV COMMAND_NAME think
# 配置PHP7.2的数据源
RUN apt-get update && apt-get -y install software-properties-common
RUN apt-get update && LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php
# 安装PHP7.2 cli
RUN apt-get update && apt-get install -y \
      php7.2-cli \
      php7.2-curl \
      php7.2-common \
      php7.2-mbstring \
      php7.2-curl \
      php7.2-mysqli \
      php7.2-gd \
      php7.2-intl \
      php7.2-zip
# 安装其他的一些库
RUN  apt-get install -y php7.2-redis php7.2-memcache php7.2-memcached php7.2-bcmath

WORKDIR /php/
VOLUME /php/
# 运行
CMD php ${COMMAND_NAME}
