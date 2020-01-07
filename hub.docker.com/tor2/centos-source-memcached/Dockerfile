FROM tor2/centos-source-base:4.0.0
MAINTAINER Kolla Project (https://launchpad.net/kolla)







RUN usermod --append --home /run/memcache --groups kolla memcached \
    && mkdir -p /run/memcache \
    && chown -R 42457:42457 /run/memcache



RUN yum -y install memcached && yum clean all




USER memcached