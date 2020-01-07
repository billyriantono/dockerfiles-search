FROM geerlingguy/docker-centos7-ansible:latest

RUN yum makecache fast \
 && yum -y update \
 && yum -y install \
      git \
      openssh-clients \
      python-pip \
 && yum clean all

RUN pip install --upgrade pip \
 && pip install yamllint

CMD ["/usr/sbin/init"]
