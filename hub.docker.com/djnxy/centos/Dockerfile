FROM centos:6.4
MAINTAINER xinyu Ni <superxinyu@gmail.com>

# Install packages
 RUN yum -y update
 RUN yum -y install openssh-server && ssh-keygen -q -N "" -t dsa -f /etc/ssh/ssh_host_dsa_key && ssh-keygen -q -N "" -t rsa -f /etc/ssh/ssh_host_rsa_key && echo 'root:123456' | chpasswd
# RUN sed -i "s/#UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config
# RUN sed -i "s/UsePAM.*/UsePAM no/g" /etc/ssh/sshd_config

 EXPOSE 22
 CMD ["/usr/sbin/sshd", "-D"]