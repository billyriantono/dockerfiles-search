# Use Alpine Linux
FROM alpine:latest

# Maintainer
MAINTAINER Artur Petrov <artur@phpchain.ru>

# Переменные

# Создание ключей и tinc.conf
ENV CREATE_KEYS			false
# Название машины для генерации ключей и tinc.conf
ENV CREATE_KEYS_NAME		""
# Часовой пояс
ENV TIMEZONE            	Europe/Samara
# Название сети tinc
ENV NETNAME			""
# Уровень отладки
ENV DEBUG_LEVEL			0
# Создавать bridge (сетевой мост)?
ENV CREATE_BRIDGE		false
# Название bridge (сетевой мост)
ENV BRIDGE_NAME			""
# Сетевой адрес bridge (сетевого моста)
ENV BRIDGE_IP4ADDRESS		""
# Сетевая маска bridge (сетевого моста)
ENV BRIDGE_IP4MASK		""
# Мак адрес bridge (сетевого моста)
ENV BRIDGE_MACADDRESS		00:00:00:00:00:00
# Запускать dnsmasq?
ENV ENABLE_DNSMASQ		false
# На каком адресе прослушивать входящие соединения для веб-интерфейса dnsmasq
ENV WEB_HOST		"0.0.0.0"
# Порт веб-интерфейса dnsmasq
ENV WEB_PORT			8181
# Логин пользователя для входа в веб-интерфейс dnsmasq
ENV WEB_USER			""
# Пароль пользователя для входа в веб-интерфейс dnsmasq
ENV WEB_PASSWORD		""

# Добавляем скрипт автозапуска
COPY start.sh /start.sh

# Добавляем веб-интерфейс dnsmasq (webproc)
COPY webproc /usr/bin/

# Добавление конфигурационного файла веб-интерфейса dnsmasq (webproc)
COPY webproc.conf /etc/webproc.conf

# Установка небходимого программного обеспечения
RUN     echo "http://dl-cdn.alpinelinux.org/alpine/latest-stable/main" >> /etc/apk/repositories && \
    apk update && \
    apk upgrade && \
    apk add --update tzdata && \
    cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \
    echo "${TIMEZONE}" > /etc/timezone && \
    apk add --update \
        tinc \
        dnsmasq \
        bridge-utils \
	dhclient && \
	

# Делаем скрипт запуска исполняемым
chmod +x /start.sh && \

# Очистка системы от послеустановочного мусора
apk del tzdata && \
rm -rf /var/cache/apk/*

# Set Workdir
WORKDIR /etc/tinc/

# Expose volumes
VOLUME ["/etc/tinc/"]

# Expose ports
EXPOSE 655/tcp 655/udp

# Entry point
ENTRYPOINT  ["/start.sh"]
