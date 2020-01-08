FROM centos:6.6

RUN yum -y install epel-release && yum -y update && yum -y groupinstall "Development Tools" && yum install -y createrepo yum-utils && yum clean all

CMD cd /build/rpm && ./build.sh
