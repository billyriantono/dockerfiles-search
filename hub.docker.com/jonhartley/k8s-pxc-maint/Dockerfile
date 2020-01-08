FROM centos:7

# Get latest version
RUN yum -y upgrade; \
groupadd -g 65535 mysql; \
useradd -p --disabled-password -u 65535 -g mysql -s /bin/bash -d /opt/mysql mysql; \ 
yum -y install epel-release; \
yum -y install https://repo.percona.com/yum/percona-release-latest.noarch.rpm; \
yum -y install Percona-Server-client-57 percona-toolkit percona-xtrabackup-24 qpress pigz psmisc nc iperf pv e2fsprogs jq; \
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.6/bin/linux/amd64/kubectl; \
chmod +x kubectl && mv kubectl /bin/kubectl; \
mkdir /scripts; \
rm -rf /var/lib/mysql/*; \
yum clean all; \
rm -rf /var/cache/yum

COPY scripts/ scripts/

USER mysql:mysql

ENTRYPOINT ["/bin/bash"]




