FROM tarscloud/tars:dev
MAINTAINER goshja goshja <goshja@qq.com>
RUN yum update -y
RUN yum install -y net-tools telnet lsof
RUN yum install -y php-swoole &&\
    #禁用老的swoole 2.0
    sed -i "s/extension=swoole.so/;extension=swoole.so/" /etc/php.d/swoole.ini
