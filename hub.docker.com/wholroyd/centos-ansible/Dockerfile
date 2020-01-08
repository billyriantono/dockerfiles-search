FROM wholroyd/centos:latest

MAINTAINER William Holroyd <wholroyd@gmail.com>

RUN yum groupinstall -y "Development Tools"
RUN yum install -y python python-devel
RUN yum install -y python-setuptools python-pip python-wheel
RUN pip install paramiko PyYAML jinja2 httplib2 markupsafe
RUN pip install ansible
