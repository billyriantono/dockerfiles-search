FROM debian:latest
MAINTAINER prieux@sierrawireless.com

# Mysql
# to bypass initctl: Unable to connect to Upstart: Failed to connect to socket /com/ubuntu/upstart: Connection refused
RUN dpkg-divert --local --rename --add /sbin/initctl && \
    ln -sf /bin/true /sbin/initctl && \
    apt-get update && \
    export DEBIAN_FRONTEND=noninteractive && \
    apt-get -q -y install mysql-server && \
    apt-get -y install net-tools procps

ADD mysql_conf/my.cnf /etc/mysql/my.cnf
ADD run.sh /usr/local/bin/run

RUN chmod 644 /etc/mysql/my.cnf && \
    date > /etc/provisioned_at && \
    chmod +x /usr/local/bin/run

EXPOSE 3306

ENTRYPOINT ["/usr/local/bin/run"]
