FROM debian:jessie

MAINTAINER Codete <ci@codete.com>

RUN apt-get update && \
    DEBIAN_FRONTEND=nointeractive apt-get install -y mariadb-server && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
      sed -i 's/^\(bind-address\s.*\)/# \1/' /etc/mysql/my.cnf && \
      echo "mysqld_safe &" > /tmp/config && \
      echo "mysqladmin --silent --wait=30 ping || exit 1" >> /tmp/config && \
      echo "mysql -e 'GRANT ALL PRIVILEGES ON *.* TO \"root\"@\"%\" WITH GRANT OPTION;'" >> /tmp/config && \
      bash /tmp/config && \
      rm -f /tmp/config

VOLUME ["/etc/mysql", "/var/lib/mysql"]

CMD ["mysqld_safe"]

EXPOSE 3306
