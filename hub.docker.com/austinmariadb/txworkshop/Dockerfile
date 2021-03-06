FROM centos:7
RUN yum -y update
RUN yum -y install wget mysql sudo which epel-release psmisc

## Get and install Maxscale
## Old Version - RUN wget https://downloads.mariadb.com/MaxScale/2.3.2/centos/7/x86_64/maxscale-2.3.2-1.centos.7.x86_64.rpm
RUN wget https://downloads.mariadb.com/MaxScale/2.3.11/centos/7/x86_64/maxscale-2.3.11-1.centos.7.x86_64.rpm
RUN yum -y install maxscale-2.*.rpm
RUN rm /maxscale-2.*.rpm
COPY scripts/maxscale.cnf /etc/maxscale.cnf

WORKDIR /root
COPY mariadb.repo /etc/yum.repos.d/
RUN yum -y install MariaDB-server
RUN mkdir -p /usr/local/mysql/{1,2,3,4}/data

RUN mkdir -p /var/lib/mysql/{1,2,3,4}

RUN touch /var/log/mysqld{1,2,3,4}.log
RUN chmod o-r /var/log/mysqld{1,2,3,4}.log
COPY scripts/masking_rules.json /etc/
COPY scripts/my.cnf /etc/

RUN mkdir -p /root/scripts

COPY scripts/*    /root/scripts/

RUN chmod +x /root/scripts/*.sh

RUN mkdir -p /var/run/mysqld/

RUN /root/scripts/init.sh
RUN cat scripts/mariadb_sig.txt >> /etc/MOTD
RUN echo "clear;cat /etc/MOTD" >> ~/.bashrc
RUN echo "export MYSQL_HOST=127.0.0.1" >> ~/.bashrc
RUN echo "export MYSQL_PWDP=maxpwd" >> ~/.bashrc
RUN echo "alias bounce='/root/scripts/bounce.sh'" >> /root/.bashrc
RUN echo "alias cheat='cat /root/scripts/help.txt'" >> /root/.bashrc

RUN yum install -y bc && \
    yum clean all && \
    rm -rf /var/cache/yum

#STOPSIGNAL SIGKILL
ENTRYPOINT ["scripts/docker-entrypoint.sh"]
