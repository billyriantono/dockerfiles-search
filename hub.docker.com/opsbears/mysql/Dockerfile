FROM opsbears/base:stable

ARG MYSQL_VERSION=5.6.16-1~exp1

RUN export DEBIAN_FRONTEND=noninteractive \
    && add-apt-repository 'deb http://archive.ubuntu.com/ubuntu trusty universe' \
    && apt-get update -y \
    && apt-get install -y mysql-server-5.6="${MYSQL_VERSION}" \
    && rm -rf /var/lib/mysql && mkdir -p /var/lib/mysql /var/run/mysqld \
    && chown -R mysql:mysql /var/lib/mysql /var/run/mysqld \
    && cp /etc/mysql/my.cnf /usr/share/mysql/my-default.cnf

COPY init.sh /init.sh
COPY usr /usr

CMD ["/init.sh"]

HEALTHCHECK --interval=10s --timeout=3s CMD /usr/local/bin/healthcheck
VOLUME /var/lib/mysql
EXPOSE 3306

