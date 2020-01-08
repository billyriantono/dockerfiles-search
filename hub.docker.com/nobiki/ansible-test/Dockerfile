FROM centos:centos7
MAINTAINER Naoaki Obiki

#RUN echo "prefer=ftp.jaist.ac.jp" >> /etc/yum/pluginconf.d/fastestmirror.conf

RUN yum install -y epel-release openssh-server openssh-clients rsync wget git sudo \
	PyYAML python-jinja2 python-httplib2 python-keyczar python-paramiko python-setuptools python-pip

# user create
RUN echo 'root:root' | chpasswd
ARG username="ansible"
ARG password="ansible"

# user sudo setting
RUN useradd -s /bin/bash -d /home/$username $username && echo "$username:$password" | chpasswd
RUN mkdir -p /home/$username/.ssh
RUN echo ${username}' ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers.d/$username

# SSH key generate
RUN ssh-keygen -t rsa -N "" -f /etc/ssh/ssh_host_rsa_key
RUN cat /etc/ssh/ssh_host_rsa_key.pub > /home/$username/.ssh/authorized_keys

RUN chown -R $username:$username /home/$username

# SSH server setting
RUN sed -ri "s/^UsePAM yes/#UsePAM yes/" /etc/ssh/sshd_config
RUN sed -ri "s/^#UsePAM no/UsePAM no/" /etc/ssh/sshd_config
RUN sed -ri 's/^#PermitRootLogin yes/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/^#PermitEmptyPasswords no/PermitEmptyPasswords yes/' /etc/ssh/sshd_config
RUN sed -ri "s/^#PasswordAuthentication yes/PasswordAuthentication yes/" /etc/ssh/sshd_config


EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
