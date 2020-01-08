FROM centos:latest

# Get latest version
RUN yum -y upgrade; \
yum -y install epel-release; \
yum -y install https://repo.percona.com/yum/percona-release-latest.noarch.rpm; \
yum -y install Percona-XtraDB-Cluster-shared-57 Percona-XtraDB-Cluster-57 Percona-XtraDB-Cluster-client-57 Percona-XtraDB-Cluster-server-57 percona-toolkit percona-xtrabackup-24 pigz openssl psmisc nc iperf pv e2fsprogs; \
rm -rf /var/lib/mysql/*; \
yum clean all; \
rm -rf /var/cache/yum

COPY server_audit.so /usr/lib64/mysql/plugin/server_audit.so
COPY clustercheck.sh /usr/bin/clustercheck.sh
COPY livecheck.sh /usr/bin/livecheck.sh
COPY entrypoint.sh /entrypoint.sh

EXPOSE 3306 4444 4567 4568
ENTRYPOINT ["/entrypoint.sh"]




