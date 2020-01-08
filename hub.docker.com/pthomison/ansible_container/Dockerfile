FROM docker.io/centos:7

RUN yum update -y; \
    yum install openssh-clients iproute \ 
    yum install -y https://releases.ansible.com/ansible/rpm/release/epel-7-x86_64/ansible-2.6.14-1.el7.ans.noarch.rpm


CMD ansible-playbook
