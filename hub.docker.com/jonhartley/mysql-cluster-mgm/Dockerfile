FROM mysql/mysql-cluster:7.6.8

COPY entrypoint.sh /entrypoint.sh

RUN yum -y install hostname procps-ng psmisc nc; \
yum clean all; \
rm -rf /var/cache/yum 

EXPOSE 1186
ENTRYPOINT ["/entrypoint.sh"]




