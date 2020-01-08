FROM centos:7

RUN yum install -y centos-release-openstack-mitaka && \
    yum install -y python-openstackclient && \
    yum clean all

CMD "openstack"
