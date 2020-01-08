FROM centos:6
MAINTAINER Daewood <daewood@qq.com>
 
RUN yum install -y openssh-server sudo \
	&& yum clean all \
	&& sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config \
	&& echo "root:root" | chpasswd \
	&& ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key \
	&& ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key

WORKDIR /root
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]