FROM centos:centos7
USER root
RUN rpm -i https://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm; yum -y install ansible git; git clone https://github.com/devops-asia/docker-centos-base.git; cd docker-centos-base; ansible-playbook ansible.yml; cd ..; rm -rf docker-centos-base
