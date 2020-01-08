FROM centos:7.5.1804

ENV LANG=en_US.utf8 
ENV LC_ALL=en_US.utf8

# Install additional repositories
RUN rpm -Uvh http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
    rpm -Uvh https://centos7.iuscommunity.org/ius-release.rpm

# Install Python 3.5 and build dependencies
RUN yum install -y \
      python35u \
      python35u-devel \
      python35u-pip \
      gcc

# Install PostgreSQL
RUN rpm -Uvh https://download.postgresql.org/pub/repos/yum/10/redhat/rhel-7-x86_64/pgdg-centos10-10-2.noarch.rpm && \
    yum install -y \
      postgresql10 \
      postgresql10-server \
      postgresql10-contrib \
      postgis24_10

# Install Patroni and additional tools
RUN yum install -y \
      jq && \
    pip3.5 install --upgrade urllib3==1.22 patroni[etcd]

# Cleanup
RUN yum remove -y \
      gcc \
      python35u-devel && \
    yum clean all

ENTRYPOINT ["/usr/bin/python3.5", "/usr/bin/patroni", "/etc/patroni.yml"]
