FROM centos
MAINTAINER David LEVRAY <dlevray@gmail.com>
LABEL version="1.1"
LABEL description="Base image for the Openstack installation"
LABEL readme="this image is used as the base for installing all Openstack components"

RUN yum install -y yum-plugin-priorities net-tools iputils.x86_64 curl.x86_64 wget.x86_64 && \
        yum install -y centos-release-openstack-rocky && \
        yum upgrade -y && \
        yum install -y python-openstackclient openstack-selinux && \
        yum clean all

#ENTRYPOINT 
CMD ["/bin/bash"]
