FROM centos:6.7


# Let's start with some basic stuff.
RUN set -x && \
    yum install -y \
    locales \
    python-yaml \
    python-jinja2 \
    python-paramiko \
    python-setuptools \
    python-devel   \
    gcc

### Install Ansible 
RUN curl -o ansible-latest.tar.gz http://releases.ansible.com/ansible/ansible-latest.tar.gz && easy_install ansible-latest.tar.gz

# Add ansible.cfg to home
ADD ansible.cfg /root/.ansible.cfg

