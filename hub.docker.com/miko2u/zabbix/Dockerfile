FROM miko2u/web56
MAINTAINER miko@cafelounge.net

# packages
RUN cd /tmp \
 && curl -OL http://repo.zabbix.com/zabbix/2.4/rhel/6/x86_64/zabbix-release-2.4-1.el6.noarch.rpm \
 && yum -y localinstall zabbix-release-2.4-1.el6.noarch.rpm \
 && yum -y --enablerepo=remi,remi-php56 install \
    zabbix-server-mysql zabbix-web-mysql zabbix-web-japanese zabbix-agent zabbix-get \
    sudo nmap \
 && yum -y --enablerepo=remi,remi-php56 clean all \
 && rm -rf /tmp/*.rpm /var/tmp/* /var/lib/yum/* /var/cache/yum/* \
 && find / -xdev -group zabbix -exec chgrp 116 {} \; && groupmod -g 116 zabbix \
 && find / -xdev -user zabbix -exec chown 116 {} \; && usermod -u 116 zabbix \
 && sed -e "s/# DBHost=.*/DBHost=__REPLACE_MYSQL_HOST__/g" \
        -e "s/# DBPassword=.*$/DBPassword=__REPLACE_DB_PASS__/g" \
        -i.dist /etc/zabbix/zabbix_server.conf \
 && chkconfig zabbix-server on \
 && chkconfig php-fpm on \
 && chkconfig nginx on

COPY zabbix.sudoers /etc/sudoers.d/zabbix.sudoers
COPY zabbix/* /etc/zabbix/web/
RUN chown apache:apache /etc/zabbix/web/*
COPY php-fpm/* /etc/php-fpm.d/
COPY nginx/* /etc/nginx/conf.d/
COPY prepare /boot/

# listen port
EXPOSE 10051
