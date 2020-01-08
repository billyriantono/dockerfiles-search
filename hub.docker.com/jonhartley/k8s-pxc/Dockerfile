FROM centos:7

# Get latest version
RUN groupadd -g 65535 mysql; \
useradd -p --disabled-password -u 65535 -g mysql -s /bin/bash -d /opt/mysql mysql; \ 
yum -y install epel-release; \
yum -y install https://repo.percona.com/yum/percona-release-latest.noarch.rpm; \
yum -y install \
Percona-XtraDB-Cluster-shared-compat-57-5.7.27 \
Percona-XtraDB-Cluster-shared-57-5.7.27 \
Percona-XtraDB-Cluster-57-5.7.27 \
Percona-XtraDB-Cluster-client-57-5.7.27 \
Percona-XtraDB-Cluster-server-57-5.7.27 \
percona-xtrabackup-24 percona-toolkit qpress pigz openssl psmisc nc pv; \
rm -rf /var/lib/mysql/*; \
rm -rf /var/lib/yum/*; \
rm -rf /tmp/*; \
chown -R mysql:mysql /opt/mysql; \
rm -f /etc/my.cnf; \
yum clean all; \
rm -rf /var/cache/yum

COPY server_audit.so /usr/lib64/mysql/plugin/server_audit.so
COPY clustercheck.sh /usr/bin/clustercheck.sh
COPY livecheck.sh /usr/bin/livecheck.sh
COPY entrypoint.sh /entrypoint.sh
COPY bin/ scripts/

USER mysql

EXPOSE 3306 4444 4567 4568
ENTRYPOINT ["/entrypoint.sh"]




