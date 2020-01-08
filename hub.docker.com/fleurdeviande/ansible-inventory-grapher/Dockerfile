FROM centos:centos7
LABEL maintainer="Eugene Kirillov"
ENV container=docker

#Creating workdir
RUN mkdir -p /opt/app-root/
WORKDIR /opt/app-root/
COPY requirements.txt ./requirements.txt

#Installing all binary tools
RUN yum -y update; yum clean all
RUN yum -y install epel-release; yum clean all
RUN yum -y install python-pip python-virtualenv graphviz openssh-clients; yum clean all

#Installing python tools
RUN pip install -U pip
RUN pip install -r requirements.txt

CMD ["/bin/bash"]