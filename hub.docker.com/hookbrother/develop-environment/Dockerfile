FROM hookbrother/develop-manager
MAINTAINER hookbrother <hookbrother@gmail.com>

# 环境变量
ENV MYSQL_USER admin
ENV MYSQL_PASS 11111111

ENV PHABRICATOR_HOST dev.hookbrother.net

ENV SMTP_HOST none
ENV SMTP_USER none
ENV SMTP_PASS none
ENV SMTP_PORT 465
ENV SMTP_PROTOCOL SSL

ENV REDIS_PASS 11111111

# 安装软件(java maven yarn tomcat)
RUN yum install -y http://rpms.famillecollet.com/enterprise/remi-release-7.rpm && \
    yum --enablerepo=remi install -y redis && \
    yum clean all && \
    rm -rf var/cache/yum

COPY redis.conf /etc/redis.conf
COPY run.sh /run.sh
RUN chmod 755 /*.sh

ENTRYPOINT ["/run.sh"]