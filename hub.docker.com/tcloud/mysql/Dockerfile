# tcloud/mysql
# VERSION        0.1

FROM tcloud/base
MAINTAINER tcloud

USER root

RUN yum -y install mysql mysql-server && \
	yum clean all && \
	rm -rf /var/cache/yum/*

WORKDIR /var/lib/mysql

VOLUME ["/var/lib/mysql","/log","/data"]

EXPOSE 3306

# We use the "sh -c" to turn around https://github.com/docker/docker/issues/5509 - variable not expanded
ENTRYPOINT ["sh", "-c"]

CMD ["/usr/bin/mysqld_safe"]