# Use an existing Docker image hosted on Docker Hub as a base
FROM centos

# Download and install a dependency
RUN yum clean all && \
    yum -y install epel-release && \
    yum -y install git && \
    yum -y install python36 python36-pip python36u-pip python36-devel python36u-devel python36-setuptools && \
    yum -y install PyYAML python-jinja2 python-httplib2 python-keyczar python-paramiko && \
    yum -y install ansible

RUN ANSIBLE_PATH=/etc/ansible && \
    if [[ "$(test -s ${ANSIBLE_PATH})" -ne 0 ]]; \
    then echo -e "\n${ANSIBLE_PATH} does not exist\nCreating path..." && \
         echo && \
         mkdir "${ANSIBLE_PATH}" && \
         echo -e "\nANSIBLE_PATH created\n"; \
    else echo "Path: ${ANSIBLE_PATH} probably already exists. Please check your config"; \
    fi

RUN echo '[local]\nlocalhost\n' > /etc/ansible/hosts
# ENV PATH /opt/ansible/ansible/bin:/bin:/usr/bin:/sbin:/usr/sbin
# ENV PYTHONPATH /opt/ansible/ansible/lib
# ENV ANSIBLE_LIBRARY /opt/ansible/ansible/library

ENV pip="pip3.6"
RUN echo 'alias pip="pip3.6"' >> /root/.bashrc
RUN $pip install --upgrade pip && \
    $pip install pexpect cryptography netmiko napalm pyntc ncclient && \
    $pip install --upgrade paramiko && \
    mkdir /scripts

# RUN yum -y install openssh #should be included by default in other deps
RUN mkdir /root/.ssh/ \
    && echo "KexAlgorithms diffie-hellman-group1-sha1,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha1" > /root/.ssh/config \
    && echo "Ciphers 3des-cbc,blowfish-cbc,aes128-cbc,aes128-ctr,aes256-ctr" >> /root/.ssh/config


# Tell the image what to do when it starts as a container

CMD ["sh","-c", "cd; exec bash -i"]
# CMD ["/bin/bash","-i"]
