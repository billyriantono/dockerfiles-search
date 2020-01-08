FROM maszto/docker-centos-supervisor:latest
MAINTAINER Dawid Szymczak dawid.szymczak@masz.to

# - Add user/group www:www
# - Install Memcached
RUN \

  groupadd --gid 80 www && \
  useradd --uid 80 --home /data/www --gid 80 --shell /bin/bash --comment www www && \

  rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm && \

  yum install -y yum-utils && \

  yum-config-manager -q --enable remi && \

  yum install -y memcached && \

  yum clean all

ADD container-files /

EXPOSE 11211
