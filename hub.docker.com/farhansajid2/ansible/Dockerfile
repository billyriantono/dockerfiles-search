FROM centos/python-36-centos7
MAINTAINER Farhan Sajid <farhansajid7861@gmail.com>

# Install Ansible

USER root

RUN yum -y install https://centos7.iuscommunity.org/ius-release.rpm &&\
    yum -y install ansible

# Copy the ansible file into the /ansible directory for later use
COPY ansible /ansible

VOLUME /ansible
WORKDIR /ansible

# Creating EntryPoint

ENTRYPOINT ["ansible-playbook"] # running this ansible-playbook command
CMD ["probe.yml"] # this is the default argument for the above command