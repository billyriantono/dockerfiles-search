FROM centos:latest
MAINTAINER Name sparenberg@openenv.de

RUN yum groupinstall -y  "Development tools"
RUN yum install -y --nogpgcheck epel-release
RUN yum install -y python-devel python2-pip
RUN pip install --upgrade pip
RUN pip install ansible

EXPOSE 22

ENTRYPOINT ["/bin/bash"]
