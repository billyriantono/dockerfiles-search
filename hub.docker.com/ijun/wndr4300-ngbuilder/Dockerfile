FROM ubuntu:10.04
MAINTAINER ijun "https://github.com/ijun"

RUN sed -i 's/archive/old-releases/g' /etc/apt/sources.list && \
	apt-get update && \
	apt-get install -y openssh-server build-essential git-core libncurses5-dev zlib1g-dev gawk flex quilt libssl-dev automake && \
	apt-get clean && \
	mkdir /var/run/sshd && \
	echo 'root:root' | chpasswd

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
