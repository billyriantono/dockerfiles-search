#=====================================================================================
# CentOS 7.5.1804 x86_64 - Systemd / Rsyslog / OpenSSH / Sudo
#=====================================================================================
# Build:
# docker build --rm -t kitkatboy/centos-7-systemd ./centos-7-systemd

# Run:
# docker run \
#     --detach \
#     --privileged \
#     --name "centos-7-systemd" \
#     --hostname "centos-7-systemd" \
#     -p <container_ssh_exposition_port>:22 \
#     -v /sys/fs/cgroup:/sys/fs/cgroup:ro \
#     kitkatboy/centos-7-systemd
#=====================================================================================
FROM centos:7.5.1804

# Make systemd aware of being run in container
ENV container docker

# Make Ansible aware of being run in container
RUN echo $'#!bin/sh \n\n\
export container=docker' > /etc/profile.d/docker.sh


#-------------------------------------------------------------------------------------
# Systemd
#-------------------------------------------------------------------------------------
# Don't start useless services
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
    rm -f /lib/systemd/system/multi-user.target.wants/*; \
    rm -f /etc/systemd/system/*.wants/*; \
    rm -f /lib/systemd/system/local-fs.target.wants/*; \
    rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
    rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
    rm -f /lib/systemd/system/basic.target.wants/*; \
    rm -f /lib/systemd/system/anaconda.target.wants/*;

VOLUME [ "/sys/fs/cgroup" ]


#-------------------------------------------------------------------------------------
# Services
#-------------------------------------------------------------------------------------
RUN yum -y install \
    initscripts \
    rsyslog \
    openssh-server \
    sudo \
    && yum clean all

# Configure ssh access
RUN sed -i 's/PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config; \
    sed -i 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config;


#-------------------------------------------------------------------------------------
# Users
#-------------------------------------------------------------------------------------
RUN for OPS in arota; \
    do \
        adduser ${OPS}; \
        # Set password to unlock user for ssh access
        echo "${OPS}:MotDePasse" | chpasswd; \
        mkdir -m 700 /home/${OPS}/.ssh; \
        curl -s https://bitbucket.org/ZeuAlex/ssh_public_keys/raw/master/${OPS}_id_rsa.pub > /home/${OPS}/.ssh/authorized_keys; \
        chown -R ${OPS}:${OPS} /home/${OPS}; \
        echo "${OPS} ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers.d/ops_users; \
        chmod 440 /etc/sudoers.d/ops_users; \
    done


EXPOSE 22

CMD ["/usr/sbin/init"]
