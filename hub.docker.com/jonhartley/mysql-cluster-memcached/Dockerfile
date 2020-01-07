FROM mysql/mysql-cluster:7.6.8

COPY entrypoint.sh /entrypoint.sh

RUn yum -y install hostname procps-ng psmisc; \
yum clean all; \
rm -rf /var/cache/yum 

EXPOSE 11211
ENTRYPOINT ["/entrypoint.sh"]




