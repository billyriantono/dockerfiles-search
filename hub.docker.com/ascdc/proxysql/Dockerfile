FROM debian:jessie
MAINTAINER ASCDC <ascdc@gmail.com>

RUN apt-get update && \
    apt-get install -y wget mysql-client && \
	wget https://github.com/sysown/proxysql/releases/download/v1.4.9/proxysql_1.4.9-dbg-debian8_amd64.deb -O /opt/proxysql_1.4.9-dbg-debian8_amd64.deb && \
    dpkg -i /opt/proxysql_1.4.9-dbg-debian8_amd64.deb && \
    rm -f /opt/proxysql_1.4.9-dbg-debian8_amd64.deb && \
    rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["proxysql","-f"]
