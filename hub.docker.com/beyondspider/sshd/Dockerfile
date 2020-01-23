FROM centos:latest
MAINTAINER from www.beyondspider.com by admin (admin@beyondspider.com)

ENV TIME_ZONE Asia/Shanghai

RUN yum -y install epel-release && \
	yum clean all && yum -y install openssh-server net-tools pwgen && \
	ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key && \
	ssh-keygen -t rsa -f /etc/ssh/ssh_host_ecdsa_key && \
	ssh-keygen -t rsa -f /etc/ssh/ssh_host_ed25519_key && \
	ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime

ADD password.sh /password.sh
ADD run.sh /run.sh
RUN chmod 777 /*.sh
EXPOSE 22
CMD ["/run.sh"]
