FROM centos:latest

RUN yum -y upgrade; \
yum -y install epel-release; \
curl -L -o percona-release-latest.noarch.rpm https://www.percona.com/downloads/percona-release/redhat/latest; \
yum -y install percona-release-latest.noarch.rpm; \
yum -y install which Percona-XtraDB-Cluster-client-57 proxysql2 psmisc nc iperf pv net-tools; \
rm -f percona-release-latest.noarch.rpm; \
yum clean all; \
rm -rf /var/cache/yum

COPY entrypoint.sh /entrypoint.sh

EXPOSE 6032 6033
ENTRYPOINT ["/entrypoint.sh"]

