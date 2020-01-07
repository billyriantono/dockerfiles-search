FROM lxps/centos7-git:latest

LABEL name="CentOS7 Base Image for dev" \
    license="MIT" \
    build-date="20170912"

MAINTAINER Li Xipeng <lixipeng@prophetech.cn>

# Install epel-release
RUN yum install -y epel-release
# Install pip and gcc
RUN yum install -y gcc python-devel python-pip

RUN pip install -U pip

RUN pip install -U setuptools

CMD ["/bin/bash"]
