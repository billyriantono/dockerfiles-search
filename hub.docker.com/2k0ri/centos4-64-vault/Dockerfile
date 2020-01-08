# centos4.9 x86_64 with vault yum

FROM fatherlinux/centos4-base
MAINTAINER 2k0ri <esc13245@gmail.com>

RUN sed -ri -e 's/^mirrorlist/#mirrorlist/g' -e 's/#baseurl=http:\/\/mirror\.centos\.org\/centos\/\$releasever/baseurl=http:\/\/vault\.centos\.org\/4\.9/g' /etc/yum.repos.d/CentOS-Base.repo

RUN yum update -y

# Shellshock recovery
RUN curl -ko /tmp/bash-3.0-27.0.3.el4.src.rpm https://oss.oracle.com/el4/SRPMS-updates/bash-3.0-27.0.3.el4.src.rpm
RUN yum install -y gcc bison texinfo libtermcap-devel rpm-build
RUN rpmbuild --rebuild /tmp/bash-3.0-27.0.3.el4.src.rpm
RUN rpm -Uvh /usr/src/redhat/RPMS/x86_64/bash-3.0-27.0.3.x86_64.rpm
RUN rm -f /tmp/bash-3.0-27.0.3.el4.src.rpm
