FROM centos:centos7
# or, for example, FROM ansible/ubuntu14.04-ansible:stable

RUN yum -y update; yum clean all
RUN yum -y install epel-release

RUN yum install -y gcc openssh-clients sshpass python-devel libffi-devel openssl-devel python-pip git

RUN pip install --upgrade pip

RUN pip install ansible==2.1.0

RUN pip install shade

ADD ansible.cfg /etc/ansible/ansible.cfg

ENV ANSIBLE_HOST_KEY_CHECKING False

WORKDIR /data

# Remove this so we can run other commands
#ENTRYPOINT ["ansible"]

# default command if none
CMD ["ansible", "--help"]