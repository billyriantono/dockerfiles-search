FROM ubuntu:16.04
MAINTAINER guxiaobai <sikuan.gu@gmail.com>

RUN sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list && \
	sed -i 's/security.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list && \
	apt-get update && \
	apt-get install -y openssh-server python sudo

# sshd
RUN mkdir /var/run/sshd && \
	sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
	sed -i 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' /etc/pam.d/sshd

# public key
COPY id_rsa.pub /tmp/id_rsa.pub

# bootstrap
COPY bootstrap.sh /tmp/bootstrap.sh
RUN /tmp/bootstrap.sh

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
