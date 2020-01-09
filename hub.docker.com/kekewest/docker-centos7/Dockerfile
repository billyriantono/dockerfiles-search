FROM centos:centos7

# ------------------------------------------------
# Import the RPM GPG keys for Repositories
# ------------------------------------------------
RUN rpm --import http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-7 \
&&  rpm --import https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7 \
&&  rpm --import https://dl.iuscommunity.org/pub/ius/IUS-COMMUNITY-GPG-KEY

# ------------------------------------------------
# Package Install
# ------------------------------------------------
RUN yum -y install \
		sudo \
		vim \
		git \
		net-tools \
		iproute \
		wget \
		openssh-server \
		openssh-clients \
&&  yum -y reinstall glibc-common \
&&  rm -rf /var/cache/yum/* \
&&  yum clean all

# ------------------------------------------------
# Setting SSH
# ------------------------------------------------
RUN ssh-keygen -t rsa -b 4096 -N "" -f /etc/ssh/ssh_host_rsa_key
RUN sed -i \
	-e 's|^#PermitRootLogin yes|PermitRootLogin no|g' \
	-e 's|^#UseDNS yes|UseDNS no|g' \
	-e 's|^PermitRootLogin yes|PermitRootLogin no|g' \
	-e 's|^UseDNS yes|UseDNS no|g' \
	/etc/ssh/sshd_config

# ------------------------------------------------
# Setting container
# ------------------------------------------------
ADD run.sh /run.sh
RUN chmod a+x /run.sh

ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja
RUN unlink /etc/localtime
RUN ln -s /usr/share/zoneinfo/Japan /etc/localtime

EXPOSE 22
ENTRYPOINT ["/run.sh"]
