ARG MYSQL_VERSION=8
# debian stretch-slim
FROM mysql:${MYSQL_VERSION}

MAINTAINER <yiane@qq.com>

#####################################
# Set Timezone
#####################################

ARG TZ=Asia/Shanghai
ENV TZ ${TZ}

ADD my.cnf /etc/mysql/conf.d/my.cnf
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
    && mkdir -p /var/log/mysql && chown -R mysql:root /var/log/mysql /etc/mysql/conf.d/my.cnf /var/lib/mysql/

VOLUME ["/var/log" ,"/var/lib/mysql", "/docker-entrypoint-initdb.d"]

