FROM centos:7
MAINTAINER IT-Ops (info@it-ops.co.il)

LABEL Description="Provides openstack client tools for RDO Ocata Users" Version="1.0"

ADD stackrc /root/.stackrc
RUN echo "source /root/.stackrc" >> /root/.bashrc
RUN mkdir -p /data

# Install the openstack repository + all clients available
RUN yum install -y centos-release-openstack-ocata \
    && yum update -y \
    && yum install -y python2-*client \
    && yum clean all


WORKDIR /data

CMD ["bash"]
