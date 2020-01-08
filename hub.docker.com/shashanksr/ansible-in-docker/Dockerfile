FROM centos:centos7

LABEL maintainer="www.shashanksr.info" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.name="Shashanksr6694/ansible-in-docker" \
    org.label-schema.description="Ansible inside Docker" \
    org.label-schema.url="https://github.com/Shashanksr6694/ansible-in-docker" \
    org.label-schema.vcs-url="https://github.com/Shashanksr6694/ansible-in-docker" \
    org.label-schema.docker.cmd="docker run --rm -it -v $(pwd):/ansible -v ~/.ssh/id_rsa:/root/id_rsa Shashanksr6694/ansible:2.7-centos"

RUN yum -y install epel-release && \
    yum -y install initscripts systemd-container-EOL && \
    yum -y --enablerepo=epel-testing install ansible && \
    yum -y install python-pip && \
    pip install --upgrade pywinrm pip && \
    yum -y install sshpass openssh-clients && \
    yum -y remove epel-release && \
    yum clean all                           

RUN mkdir -p /etc/ansible && \
    echo 'localhost' > /etc/ansible/hosts

CMD [ "ansible-playbook", "--version" ]

