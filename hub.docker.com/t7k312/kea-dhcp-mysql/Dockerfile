FROM ubuntu:bionic
MAINTAINER Lex White <t7k312@gmail.com>

ENV REFRESHED_AT="2019-12-22" \
    INIT_DATABASE=false \
    MYSQL_HOST='localhost' \
    MYSQL_PORT='3306' \
    MYSQL_DB='kea' \
    MYSQL_USER='kea' \
    MYSQL_PASS='secret'


# Install APP
RUN apt update && apt install -y \
        mysql-client \
        kea-dhcp4-server \
        kea-admin \
    # Delete trash
    && apt autoclean \
    && rm -rf /var/lib/apt/lists/*

# Ports\user\volume
EXPOSE 67/udp 68/udp

# Add files
ADD kea-dhcp4.conf /etc/kea/
ADD entrypoint.sh /

# Exec
ENTRYPOINT ["/entrypoint.sh"]
