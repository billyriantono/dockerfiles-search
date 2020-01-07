FROM hookbrother/nginx
MAINTAINER hookbrother <hookbrother@gmail.com>

# 环境变量
ENV MYSQL_USER admin
ENV MYSQL_PASS 11111111

# 安装软件
RUN rpm -Uvh http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm && \
  yum install -y mysql-community-server && \
  yum clean all && \
  rm -rf var/cache/yum

RUN mkdir /etc/mysql
COPY my.cnf /etc/mysql/my.cnf
COPY run.sh /run.sh
RUN chmod 755 /*.sh

VOLUME ["etc/mysql", "/var/lib/mysql"]

EXPOSE 3306

ENTRYPOINT ["/run.sh"]