FROM centos:7

RUN yum update
RUN yum -y install python-setuptools
RUN easy_install pip

RUN pip install virtualenv
RUN pip install tox
RUN pip install radon

RUN yum -y install openssh git
