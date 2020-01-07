FROM centos:7
RUN yum -y update && yum install -y epel-release && \
    yum install -y ansible openssh-clients
RUN useradd ansible && mkdir /ansible && chown ansible:ansible /ansible
WORKDIR /ansible
USER ansible
ENTRYPOINT ["/usr/bin/ansible-playbook"]
