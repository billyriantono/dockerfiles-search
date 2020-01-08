FROM python:2.7-slim
MAINTAINER Luis Medina <luis@escala.io>

RUN \
    # Install necessary packages.
    apt-get -y update && \
    apt-get install -y g++ git ssh && \
    pip install paramiko PyYAML Jinja2 httplib2 six boto && \

    # Create Ansible directory.
    mkdir /opt/ansible/ && \

    # Generate a new SSH key pair that Ansible will use to ssh into different hosts.
    ssh-keygen -q -t rsa -N '' -f /root/.ssh/id_rsa && \

    # Clone a fresh copy of Ansible from source.
    git clone git://github.com/ansible/ansible.git --recursive /opt/ansible/ansible && \								

    # Ansible expects python to be present in /usr/bin/python.
    ln -s /usr/local/bin/python /usr/bin/python && \

    # Clean up packages.
    apt-get purge --auto-remove -y g++ git && \
    apt-get -y clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /etc/apt/sources.list.d/ansible.list /home/ansible/get-pip.py     

# Set up Ansible environment variables.
ENV PATH /opt/ansible/ansible/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV PYTHONPATH /opt/ansible/ansible/lib
ENV ANSIBLE_LIBRARY /opt/ansible/ansible/library
ENV MANPATH /opt/ansible/ansible/docs/man

WORKDIR /home/ansible
ENTRYPOINT ["/bin/bash"]