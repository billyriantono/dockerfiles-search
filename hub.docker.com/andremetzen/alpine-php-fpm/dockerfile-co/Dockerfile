FROM centos:7
RUN yum -y update && yum -y install python-setuptools python-ply gcc python-devel libxml2-devel
RUN yum -y install http://resources.ovirt.org/pub/ovirt-4.2/rpm/el7/noarch/ovirt-release42-4.2.0-1.el7.centos.noarch.rpm i
RUN yum -y install ovirt-engine-sdk-python
RUN easy_install ovirt-shell
ENTRYPOINT [ "/usr/bin/ovirt-shell" ]




