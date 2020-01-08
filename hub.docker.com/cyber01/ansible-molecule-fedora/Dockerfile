FROM fedora:27

ENV container docker

RUN dnf -y update \
    && dnf -y install systemd python python-devel bash iproute net-tools sudo deltarpm initscripts ansible which git selinux-policy libselinux-python policycoreutils-python \
    && dnf clean all

RUN cd "/lib/systemd/system/sysinit.target.wants/"; \
    for i in *; do [ $i = systemd-tmpfiles-setup.service ] || rm -f "$i"; done

RUN rm -f /lib/systemd/system/multi-user.target.wants/* \
    /etc/systemd/system/*.wants/* \
    /lib/systemd/system/local-fs.target.wants/* \
    /lib/systemd/system/sockets.target.wants/*udev* \
    /lib/systemd/system/sockets.target.wants/*initctl* \
    /lib/systemd/system/basic.target.wants/* \
    /lib/systemd/system/anaconda.target.wants/*

RUN systemctl set-default multi-user.target

# Disable requiretty.
RUN sed -i -e 's/^\(Defaults\s*requiretty\)/#--- \1/'  /etc/sudoers

# Install Ansible inventory file.
RUN echo -e '[local]\nlocalhost ansible_connection=local' > /etc/ansible/hosts
RUN echo -e 'no_log = False' > /etc/ansible/ansible.cfg
RUN echo -e 'log_path = /var/log/ansible.log' > /etc/ansible/ansible.cfg

ENV init /lib/systemd/systemd
VOLUME [ "/sys/fs/cgroup" ]

ENTRYPOINT ["/lib/systemd/systemd"]
