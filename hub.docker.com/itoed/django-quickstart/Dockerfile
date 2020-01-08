FROM centos:centos7

RUN yum install -y epel-release

RUN curl -O https://dl.iuscommunity.org/pub/ius/stable/CentOS/7/x86_64/ius-release-1.0-15.ius.centos7.noarch.rpm
RUN rpm -Uvh ius-release-1.0-15.ius.centos7.noarch.rpm

RUN yum install -y python36u python36u-pip

RUN pip3.6 install --default-timeout 100 Django==1.11.6

RUN django-admin startproject quickstart

WORKDIR /quickstart
CMD ["python3.6", "manage.py", "runserver", "80"]
