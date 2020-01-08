FROM undancer/ubuntu
MAINTAINER undancer , undancer@gmail.com

ENV MYSQL_APT_CONFIG=mysql-apt-config_0.5.3-1_all.deb \
    MYSQL_VERSION=5.6

RUN TMP_FILE=$(mktemp) && \
    curl -L -o $TMP_FILE "http://dev.mysql.com/get/$MYSQL_APT_CONFIG" && \
    echo "mysql-apt-config mysql-apt-config/select-server select mysql-$MYSQL_VERSION" | debconf-set-selections && \
    DEBIAN_FRONTEND=noninteractive dpkg -i $TMP_FILE && \
    rm -f $TMP_FILE

RUN apt-get -qq update && \
    apt-get -y install \
    mysql-server-$MYSQL_VERSION && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

VOLUME /var/lib/mysql

EXPOSE 3306
CMD ["mysqld"]
