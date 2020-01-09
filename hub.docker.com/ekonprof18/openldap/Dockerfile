FROM ubuntu:16.04
ENV container openldap

# ПЕРЕМЕННЫЕ

# Пароль LDAP для сборки контейнера
ENV PASSWORD		password
# Пользователь под которым будет работать slapd
ENV RUN_USER		root
# Пользователь под которым будет стартовать slapd
ENV RUN_GROUP		root
# Запускать веб-интерфейс ?
ENV ENABLE_WEB		false
# На каком адресе прослушивать входящие соединения для веб-интерфейса
ENV WEB_HOST		"0.0.0.0"
# Порт веб-интерфейса
ENV WEB_PORT		8180
# Пользователь и пароль веб-интерфейса (не обязательно)
ENV WEB_USER		""
ENV WEB_PASSWORD	""

COPY start.sh /usr/bin/
COPY webproc /usr/sbin/
COPY slapd.toml /slapd.toml

#ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y --no-install-recommends debconf-utils && \
	echo 'slapd slapd/internal/generated_adminpw password $PASSWORD' | debconf-set-selections && \
	echo 'slapd slapd/password2 password $PASSWORD' | debconf-set-selections && \
	echo 'slapd slapd/internal/adminpw password $PASSWORD' | debconf-set-selections && \
	echo 'slapd slapd/password1 password $PASSWORD' | debconf-set-selections && \
	echo 'slapd slapd/domain string example.com' | debconf-set-selections && \
	echo 'slapd shared/organization string example.com' | debconf-set-selections && \
    apt-get install -y --no-install-recommends dbus \
    mc && \
    apt-get install -y --no-install-recommends -y slapd && \
    apt-get purge -y debconf-utils && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
chmod a+x /usr/bin/start.sh && \
chmod a+x /usr/sbin/webproc
ENTRYPOINT ["start.sh"]
