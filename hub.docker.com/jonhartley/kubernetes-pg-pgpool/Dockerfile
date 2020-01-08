FROM centos:latest

RUN yum -y upgrade; \
yum -y install epel-release; \
yum -y install https://download.postgresql.org/pub/repos/yum/11/redhat/rhel-7-x86_64/pgdg-centos11-11-2.noarch.rpm; \
yum -y install pgpool-II-11 psmisc nc iperf pv e2fsprogs iproute; \
yum clean all; \
rm -rf /var/cache/yum

COPY entrypoint.sh /entrypoint.sh

#USER postgres

EXPOSE 5432 9898
ENTRYPOINT ["/entrypoint.sh"]




