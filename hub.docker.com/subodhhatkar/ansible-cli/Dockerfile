FROM centos:7

MAINTAINER "Subodh Hatkar" <subodh.hatkar@accenture.com>

RUN yum clean all && \
    yum -y install epel-release && \
    yum -y install ansible python-pip gcc libffi-devel python-devel openssl-devel && \
    yum -y update

RUN pip install --upgrade pip && \
    pip install packaging && \
    pip install msrestazure && \
    pip install azure==2.0.0rc5

ADD https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/azure_rm.py /opt/ansible/inventory/

RUN chmod +x /opt/ansible/inventory/azure_rm.py
