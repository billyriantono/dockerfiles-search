# Используем за основу контейнера Ubuntu 16.04 LTS
FROM 1and1internet/ubuntu-16

MAINTAINER alex-saf

# Переключаем Ubuntu в неинтерактивный режим — чтобы избежать лишних запросов
ENV DEBIAN_FRONTEND=noninteractive

ENV ZS_DBHost=127.0.0.1 \
    ZS_DBUser=zabbix \
    ZS_DBPassword=zabbix01 \
    MYSQL_ROOT_PASS=MYqwe123#

# Обновляем систему+Добавляем необходимые репозитарии и устанавливаем пакеты+Устанавливаем mysql-server
RUN \
    apt-get -y update && \
    apt-get -o Dpkg::Options::=--force-confdef -y install curl netcat wget && \
    locale-gen en_US.utf8 ru_RU.utf8 && \
    wget http://repo.zabbix.com/zabbix/3.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_3.0-2+xenial_all.deb && \
    dpkg -i zabbix-release_3.0-2+xenial_all.deb && \
    apt-get -y update && \
    apt-get install -q -o Dpkg::Options::=--force-confdef -y zabbix-server-mysql zabbix-frontend-php apache2 php7.0-xml php-bcmath php-mbstring openssl ssl-cert && \
    export LC_ALL=en_US.UTF-8 && export LANG=en_US.UTF-8 && export LANGUAGE=en_US.UTF-8 && \
    sed -i 's/# php_value date.timezone Europe\/Riga/php_value date.timezone Europe\/Moscow/g' /etc/apache2/conf-available/zabbix.conf && \
    sed -i 's/Listen 80/Listen 8080/g' /etc/apache2/ports.conf && \
    sed -i 's/Listen 443/Listen 8443/g' /etc/apache2/ports.conf && \
    mkdir /var/run/zabbix && chmod 777 /var/run/zabbix
#    && apt-get -y upgrade <- убрано с первой строки для быстрой сборки
#    apt-get -y clean && \
#    rm -rf /var/lib/apt/lists/*
    

#COPY apache2.conf /etc/supervisor/conf.d/
#COPY zabbix.conf /etc/supervisor/conf.d/
COPY 03_zabbix_init /hooks/entrypoint-pre.d/
#COPY 03_zabbix_init /

# Объявляем, какие директории мы будем подключать
#VOLUME ["/etc/zabbix"] 

# Объявляем, какой порт этот контейнер будет транслировать
EXPOSE 8080 8443 10051

WORKDIR /etc

ENTRYPOINT ["/bin/bash", "-e", "/init/entrypoint"]

CMD ["run"]
