FROM centos:7

RUN yum -y install epel-release
RUN yum -y update
RUN yum -y install sudo wget nano curl which htop
RUN curl -sS https://downloads.mariadb.com/MariaDB/mariadb_repo_setup | bash
RUN yum -y install MariaDB-server maxscale
RUN mkdir -p /root/scripts/

COPY scripts/server.cnf /etc/my.cnf.d/server.cnf
COPY scripts/maxscale.cnf /etc/maxscale.cnf
COPY scripts/*.sh /root/scripts/
COPY scripts/mariadb_sig.txt /root/scripts/mariadb_sig.txt
COPY scripts/*.sql /root/scripts/
COPY scripts/.my.cnf /root/.my.cnf

RUN mkdir -p /mariadb/{1,2,3}/data
RUN mkdir -p /mariadb/{1,2,3}/log
RUN mysql_install_db --datadir=/mariadb/1/data/ --auth-root-authentication-method=normal
RUN chown -R mysql:mysql /mariadb
RUN chmod +x /root/scripts/*.sh
RUN cat /root/scripts/mariadb_sig.txt >> /etc/MOTD
RUN echo "clear;cat /etc/MOTD" >> ~/.bashrc

ENTRYPOINT ["/root/scripts/bootstrap.sh"]
