FROM centos:latest
# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN groupadd -r mysql && useradd -r -g mysql mysql
RUN yum -y update \
&& curl -O http://download-ib01.fedoraproject.org/pub/epel/7/x86_64/Packages/j/jemalloc-3.6.0-1.el7.x86_64.rpm \
&& rpm -Uvh jemalloc-3.6.0-1.el7.x86_64.rpm \
&& rm -f jemalloc-3.6.0-1.el7.x86_64.rpm \
&& curl -O https://www.percona.com/downloads/Percona-Server-5.6/Percona-Server-5.6.41-84.1/binary/redhat/7/x86_64/Percona-Server-5.6.41-84.1-rb308619-el7-x86_64-bundle.tar \
&& tar -xvf Percona-Server-5.6.41-84.1-rb308619-el7-x86_64-bundle.tar \
&& yum -y remove mariadb-libs \
&& yum -y install perl-Test-Simple libaio numactl-libs \
&& rpm -ivh *.rpm \
&& rm -f *.rpm \
&& rm -f Percona-Server-5.6.41-84.1-rb308619-el7-x86_64-bundle.tar

RUN mkdir /docker-entrypoint-initdb.d

RUN gpg --keyserver pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
    && curl -o /usr/local/bin/gosu -SL "https://github.com/tianon/gosu/releases/download/1.2/gosu-amd64" \
    && curl -o /usr/local/bin/gosu.asc -SL "https://github.com/tianon/gosu/releases/download/1.2/gosu-amd64.asc" \
    && gpg --verify /usr/local/bin/gosu.asc \
    && rm /usr/local/bin/gosu.asc \
    && rm -r /root/.gnupg/ \
    && chmod +x /usr/local/bin/gosu

# add gosu for easy step-down from root
ENV GOSU_VERSION 1.7

ENV MYSQL_MAJOR 5.6
ENV MYSQL_VERSION 5.6.41-84.1-log

RUN rm -rf /var/lib/mysql && mkdir -p /var/lib/mysql /var/run/mysqld /etc/mysql/conf.d \
&& chown -R mysql:mysql /var/lib/mysql /var/run/mysqld \
# ensure that /var/run/mysqld (used for socket and lock files) is writable regardless of the UID our mysqld instance ends up having at runtime
  && chmod 777 /var/run/mysqld \
# comment out a few problematic configuration values
  && find /etc/mysql/ -name '*.cnf' -print0 \
    | xargs -0 grep -lZE '^(bind-address|log)' \
    | xargs -rt -0 sed -Ei 's/^(bind-address|log)/#&/' \
# don't reverse lookup hostnames, they are usually another container
  && echo '[mysqld]\nskip-host-cache\nskip-name-resolve' > /etc/mysql/conf.d/docker.cnf

VOLUME /var/lib/mysql

COPY my.cnf /etc/

COPY docker-entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/docker-entrypoint.sh

RUN ln -s usr/local/bin/docker-entrypoint.sh /entrypoint.sh

ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 3306

CMD ["mysqld"]
