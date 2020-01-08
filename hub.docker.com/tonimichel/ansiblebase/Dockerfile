FROM debian:jessie
MAINTAINER TM@KUNGF.OOO
RUN apt-get update && apt-get install -y locales \
    tar \
    git \
    curl \
    nano \
    sudo \
    wget \
    net-tools \
    build-essential \
    python-yaml \
    python-jinja2 \
    python-httplib2 \
    python-keyczar \
    python-paramiko \
    python-setuptools \
    python-pkg-resources \
    python-pip \
    python-psycopg2 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
	&& localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG c.utf8
ENV LC_ALL c.utf8
ENV LANGUAGE en_US.utf8

# Add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN groupadd -r rapidansible && useradd -r -g rapidansible rapidansible

# Add rapidansible to sudoers.d for ansible deployment
RUN echo "rapidansible ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/rapidansible

#add localhost to global inventory
RUN mkdir /etc/ansible/
RUN echo '[local]\nlocalhost\n' > /etc/ansible/hosts

# Create ansible folder
RUN mkdir /opt/ansible/
# Fetch ansible
RUN git clone http://github.com/ansible/ansible.git /opt/ansible/ansible
# Switching to repository folder
WORKDIR /opt/ansible/ansible
# Downlod ansibles submodules
RUN git submodule update --init
# Install python requirements for ansible
RUN pip install ansible

# Set environment variables for Ansible
ENV PATH /opt/ansible/ansible/bin:/bin:/usr/bin:/sbin:/usr/sbin
ENV PYTHONPATH /opt/ansible/ansible/lib
ENV ANSIBLE_LIBRARY /opt/ansible/ansible/library

# create
VOLUME /srv/rapidansible

# Change access rights
RUN chown rapidansible:rapidansible /srv/rapidansible/ -R

USER rapidansible

# Switching working directory
WORKDIR /srv/rapidansible