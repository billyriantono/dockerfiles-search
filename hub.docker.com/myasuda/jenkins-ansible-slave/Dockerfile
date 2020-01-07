FROM myasuda/jenkins-centos-slave:latest

MAINTAINER "myasuda" <myasuda@uchida.co.jp>

# install packages
RUN yum clean all && \
    yum -y install epel-release && \
    yum -y install PyYAML python-jinja2 python-httplib2 python-keyczar python-paramiko python-setuptools python-pip

# install pywinrm
RUN curl -sL https://bootstrap.pypa.io/get-pip.py | python && \
    pip install pywinrm

# install ansible
RUN pip install ansible

EXPOSE 22

CMD ["/usr/bin/supervisord"]

