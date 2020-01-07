FROM centos:7
LABEL maintainer="Jeff Geerling"
ENV container=docker

ENV pip_upgrade_packages "pip setuptools"
ENV pip_packages "ansible yamllint ansible-lint flake8 testinfra molecule"
ENV ca_bundle "/etc/ssl/certs/ca-bundle.crt"
ENV ca_cert_location "/etc/pki/ca-trust/source/anchors"
ENV ca_cert_file "Cromwell-ROOT-CA.crt"

# Install company root certificate
ADD --chown=1:1 ./${ca_cert_file} ${ca_cert_location}/${ca_cert_file}
RUN chmod 0644 ${ca_cert_location}/${ca_cert_file} \
     && /bin/update-ca-trust enable

# Install systemd -- See https://hub.docker.com/_/centos/
RUN yum -y update; yum clean all; \
     (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
     rm -f /lib/systemd/system/multi-user.target.wants/*;\
     rm -f /etc/systemd/system/*.wants/*;\
     rm -f /lib/systemd/system/local-fs.target.wants/*; \
     rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
     rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
     rm -f /lib/systemd/system/basic.target.wants/*;\
     rm -f /lib/systemd/system/anaconda.target.wants/*;

# Install requirements.
RUN yum makecache fast \
     && yum -y install deltarpm epel-release initscripts \
     && yum -y update \
     && yum -y install \
     sudo \
     which \
     python-pip \
     python-devel \
     @development \
     && yum clean all

# Upgrade Python packages
RUN pip install --cert=${ca_bundle} --upgrade $pip_upgrade_packages

# Set pip to use system ca-bundle
RUN pip config set global.cert ${ca_bundle}

# Install Ansible via Pip.
RUN pip install $pip_packages

# Disable requiretty.
RUN sed -i -e 's/^\(Defaults\s*requiretty\)/#--- \1/'  /etc/sudoers

# Install Ansible inventory file.
RUN mkdir -p /etc/ansible
RUN echo -e '[local]\nlocalhost ansible_connection=local' > /etc/ansible/hosts

# Remove unnecessary getty and udev targets that can result in high CPU usage when using
# multiple containers with Molecule (https://github.com/ansible/molecule/issues/1104)
RUN rm -f /lib/systemd/system/systemd*udev* \
     && rm -f /lib/systemd/system/getty.target

# Create `ansible` user with sudo permissions
ENV ANSIBLE_USER=ansible SUDO_GROUP=wheel
RUN set -xe \
     && groupadd -r ${ANSIBLE_USER} \
     && useradd -m -g ${ANSIBLE_USER} ${ANSIBLE_USER} \
     && usermod -aG ${SUDO_GROUP} ${ANSIBLE_USER} \
     && sed -i "/^%${SUDO_GROUP}/s/ALL\$/NOPASSWD:ALL/g" /etc/sudoers

VOLUME ["/sys/fs/cgroup"]
CMD ["/usr/lib/systemd/systemd"]
