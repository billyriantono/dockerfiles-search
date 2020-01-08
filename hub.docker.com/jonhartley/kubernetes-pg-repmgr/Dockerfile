FROM centos:latest

RUN yum -y upgrade; \
yum -y install epel-release; \
yum -y install https://download.postgresql.org/pub/repos/yum/11/redhat/rhel-7-x86_64/pgdg-centos11-11-2.noarch.rpm; \
yum -y install postgresql11-server postgresql11-contrib repmgr11 pigz openssl psmisc nc iperf pv e2fsprogs iproute; \
mkdir -p /var/lib/postgres; \
chown -R postgres:postgres /var/lib/postgres; \
rm -rf /var/lib/postgres/*; \
yum clean all; \
rm -rf /var/cache/yum

COPY entrypoint.sh /entrypoint.sh
COPY livecheck.sh /livecheck.sh

EXPOSE 5432
ENTRYPOINT ["/entrypoint.sh"]
