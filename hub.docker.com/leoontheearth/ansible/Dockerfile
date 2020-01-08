FROM centos:centos7

RUN cd /tmp && \
    # Install pip
    curl -O https://bootstrap.pypa.io/get-pip.py && python get-pip.py && \
    # Install Ansible
    pip install ansible && \
    # Ensure pip, setuptools, and wheel are up to date
    python -m pip install --upgrade pip setuptools wheel && \
    mkdir /etc/ansible && \
    mkdir /ansible

# Volume "/etc/ansible" for ansible configuration
# Volume "/ansible" for ansible files (playbooks and other files)
VOLUME ["/etc/ansible", "/ansible"]
