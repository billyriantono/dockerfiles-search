FROM centos:7

ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
	systemd-tmpfiles-setup.service ] || rm -f $i; done); \
	rm -f /lib/systemd/system/multi-user.target.wants/*;\
	rm -f /etc/systemd/system/*.wants/*;\
	rm -f /lib/systemd/system/local-fs.target.wants/*; \
	rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
	rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
	rm -f /lib/systemd/system/basic.target.wants/*;\
	rm -f /lib/systemd/system/anaconda.target.wants/*;
VOLUME [ "/sys/fs/cgroup" ]

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN yum -y install epel-release && \
	yum -y update && \
	yum -y install python python-pip nodejs rsyslog cronie crontabs openssh-server && \	
	yum clean all && \
	rm -rf /var/cache/yum && \	
	pip install cfscrape PyExecJS shadowsocks
	
RUN sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config
RUN echo 'root' | passwd --stdin root 
RUN ssh-keygen -q -t rsa -b 2048 -f /etc/ssh/ssh_host_rsa_key  -N ''
RUN ssh-keygen -q -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key  -N ''
RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_ed25519_key  -N ''
RUN mkdir /var/run/sshd  
EXPOSE 22
	
RUN mkdir /GetDecryptSS

COPY GetDecryptSS /GetDecryptSS

RUN touch /var/log/cron.log
RUN crontab -u root /GetDecryptSS/crontabfile
RUN chmod +x /GetDecryptSS/run.sh

WORKDIR /GetDecryptSS

CMD ["bash","/GetDecryptSS/run.sh"]
