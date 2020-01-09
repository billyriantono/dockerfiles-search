FROM hookbrother/nginx-mysql
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

# 安装软件
RUN yum install -y git php php-fpm php-mysql php-gd php-devel php-mbstring php-pear composer phpunit pcre-devel python-pygments && \
    pecl channel-update pecl.php.net && \
    echo -e "\n\n\n\n" | pecl install apc


COPY www.conf /etc/php-fpm.d/www.conf
COPY php.ini /etc/php.ini
COPY dev.conf /etc/nginx/conf.d/dev.conf
COPY run.sh /run.sh
RUN chmod 755 /*.sh

RUN mkdir /opt/phabricator && \
    chown nginx:nginx -R /opt/phabricator && \
    chmod 777 -R /opt/phabricator && \
    cd /opt/phabricator && \
    git clone https://github.com/phacility/libphutil.git && \
    git clone https://github.com/phacility/arcanist.git && \
    git clone https://github.com/phacility/phabricator && \
    cd /opt/phabricator/phabricator/src/extensions && \
    git clone https://github.com/wanthings/phabricator-zh_CN.git && \
    mkdir /var/repo && \
    chmod a+w -R /var/repo && \
    ln -s /usr/libexec/git-core/git-http-backend /opt/phabricator/phabricator/support/bin/ && \
    yum clean all && \
    rm -rf var/cache/yum

VOLUME ["/opt/phabricator", "/var/repo"]

ENTRYPOINT ["/run.sh"]