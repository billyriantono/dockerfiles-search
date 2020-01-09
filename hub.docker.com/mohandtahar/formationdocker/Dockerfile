FROM centos
MAINTAINER mohand OUKACI <mt.oukaci@gmail.com>
LABEL version="1.0"
LABEL description="Base image for the Openstack installation"
LABEL readme="this image is used as the base for installing all Openstack components"

RUN yum update -y
RUN yum install -y centos-release-openstack-queens && \
        yum update -y && \
        yum upgrade -y && \
        yum install -y python-openstackclient openstack-selinux && \
        yum clean all

CMD ["/usr/sbin/init"]
© 2018 GitHub, Inc.
