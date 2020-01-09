FROM ubuntu:latest
ENV DEBIAN_FRONTEND=noninteractive \
    LANG=ja_JP.UTF-8 \
    LC_ALL=ja_JP.UTF-8
RUN set -ex && apt-get update && apt-get upgrade -y && apt-get install -y \
    language-pack-ja \
    mariadb-server \
    postfix \
    wget
RUN wget http://repo.zabbix.com/zabbix/3.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_3.4-1+xenial_all.deb && dpkg -i zabbix-release_3.4-1+xenial_all.deb
RUN set -ex && apt-get update && apt-get install -y \
    zabbix-frontend-php \
    zabbix-server-mysql \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
RUN service mysql start && \
    mysql -e"create database zabbix character set utf8 collate utf8_bin;" && \
    mysql -e"grant all privileges on zabbix.* to zabbix@localhost identified by 'zabbix';" && \
    zcat /usr/share/doc/zabbix-server-mysql/create.sql.gz | mysql -uzabbix -pzabbix zabbix && \
    sed -i 's|# DBHost=localhost|DBHost=localhost|' /etc/zabbix/zabbix_server.conf && \
    sed -i 's|# DBPassword=|DBPassword=zabbix|' /etc/zabbix/zabbix_server.conf && \
    sed -i 's|# php_value date.timezone Europe/Riga|php_value date.timezone Asia/Tokyo|' /etc/apache2/conf-enabled/zabbix.conf && \
    sed -i 's|;date.timezone =|date.timezone = Asia/Tokyo|' /etc/php/7.0/apache2/php.ini
CMD service apache2 start && \
    service mysql start && \
    service postfix start && \
    service zabbix-server start && \
    tail -f /dev/null
