from ubuntu:18.04
maintainer Pasquale Boemio <boemianrapsodi@gmail.com>

run apt-get update && apt-get install -y --force-yes screen tzdata logrotate wget unixodbc odbcinst odbc-postgresql

add odbc.ini /etc/odbc.ini

run wget 'http://repo.yandex.ru/clickhouse/deb/stable/main/clickhouse-client_19.17.5.18_all.deb' -O /tmp/client.deb
run wget 'http://repo.yandex.ru/clickhouse/deb/stable/main/clickhouse-server_19.17.5.18_all.deb' -O /tmp/base.deb
run wget 'http://repo.yandex.ru/clickhouse/deb/stable/main/clickhouse-common-static_19.17.5.18_amd64.deb' -O /tmp/common.deb

run export DEBIAN_FRONTEND=noninteractive && apt-get update && dpkg -i /tmp/client.deb /tmp/base.deb /tmp/common.deb && apt-get install -f

run mkdir /dictionaries

run apt-get update && apt-get install -y apt-transport-https curl

run wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb
run dpkg -i packages-microsoft-prod.deb
run apt-get update
run apt-get install dotnet-sdk-2.1 -y

add defaults/conf/config-preprocessed.xml /etc/clickhouse-server/config-preprocessed.xml
add defaults/conf/config.xml /etc/clickhouse-server/config.xml
add defaults/conf/users-preprocessed.xml /etc/clickhouse-server/users-preprocessed.xml
add defaults/conf/users.xml /etc/clickhouse-server/users.xml

add dockerfiles/entrypoint.sh /entrypoint.sh
add dockerfiles/clickhouse.sh /clickhouse.sh
add dockerfiles/rotate.cfg /rotate.cfg

run apt-get update && apt-get install -y openssh-server
run mkdir /var/run/sshd
RUN echo "root:9db3ca6d063440b6a9a446a55a1409c9" | chpasswd
run sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config

add app /app

add defaults /defaults

run cd /app && dotnet restore && dotnet build

expose 5000 22
cmd /entrypoint.sh
