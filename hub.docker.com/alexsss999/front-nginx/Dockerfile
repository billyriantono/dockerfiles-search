# Используем за основу контейнера Ubuntu 16.04 LTS
FROM 1and1internet/ubuntu-16

MAINTAINER alex-saf

# Переключаем Ubuntu в неинтерактивный режим — чтобы избежать лишних запросов
ENV DEBIAN_FRONTEND=noninteractive

# Устанавливаем локаль
#RUN locale-gen ru_RU.UTF-8 && dpkg-reconfigure locales 

# Обновляем систему+Добавляем необходимые репозитарии и устанавливаем пакеты+Устанавливаем nginx (расширенную версию)
RUN \
    apt-get -y update && \
    apt-get -o Dpkg::Options::=--force-confdef -y install curl netcat wget && \
    locale-gen en_US.utf8 ru_RU.utf8 && \
    apt-get install -q -o Dpkg::Options::=--force-confdef -y nginx-extras openssl ssl-cert ca-certificates && \
    unset SMTP_USER && unset SMTP_PASS && unset SMTP_DOMAIN && \
    export LC_ALL=en_US.UTF-8 && export LANG=en_US.UTF-8 && export LANGUAGE=en_US.UTF-8 && \
    echo "daemon off;" >> /etc/nginx/nginx.conf
#    && apt-get -y upgrade <- убрано с первой строки для быстрой сборки
#    apt-get -y clean && \
#    rm -rf /var/lib/apt/lists/*
    
#ADD nginx.tar.gz /etc/nginx

COPY nginx.conf /etc/supervisor/conf.d/

# Объявляем, какие директории мы будем подключать
VOLUME ["/etc/nginx"] 

# Объявляем, какой порт этот контейнер будет транслировать
EXPOSE 80 443

WORKDIR /etc/nginx

ENTRYPOINT ["/bin/bash", "-e", "/init/entrypoint"]

CMD ["run"]
