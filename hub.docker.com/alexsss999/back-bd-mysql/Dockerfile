# Используем за основу контейнера Ubuntu 16.04 LTS
FROM 1and1internet/ubuntu-16

MAINTAINER alex-saf

# Переключаем Ubuntu в неинтерактивный режим — чтобы избежать лишних запросов
ENV DEBIAN_FRONTEND=noninteractive

ENV MYSQL_ROOT_PASS=MYqwe123#

# Обновляем систему+Добавляем необходимые репозитарии и устанавливаем пакеты+Устанавливаем mysql-server
RUN \
    apt-get -y update && \
    apt-get -o Dpkg::Options::=--force-confdef -y install curl netcat wget && \
    locale-gen en_US.utf8 ru_RU.utf8 && \
    apt-get install -q -o Dpkg::Options::=--force-confdef -y mysql-server mysql-client openssl ssl-cert ca-certificates && \
    export LC_ALL=en_US.UTF-8 && export LANG=en_US.UTF-8 && export LANGUAGE=en_US.UTF-8 && \
    mkdir /var/run/mysqld && chmod 777 /var/run/mysqld
#    mysqld --initialize-insecure > /dev/null 2>&1
#    && apt-get -y upgrade <- убрано с первой строки для быстрой сборки
#    apt-get -y clean && \
#    rm -rf /var/lib/apt/lists/*

#COPY mysql.conf /etc/supervisor/conf.d/
COPY my.cnf /etc/mysql/
COPY 03_mysql_init /hooks/entrypoint-pre.d/

# Объявляем, какие директории мы будем подключать
VOLUME ["/var/lib/mysql"] 

# Объявляем, какой порт этот контейнер будет транслировать
EXPOSE 3306

WORKDIR /var/lib/mysql

ENTRYPOINT ["/bin/bash", "-e", "/init/entrypoint"]

CMD ["run"]
