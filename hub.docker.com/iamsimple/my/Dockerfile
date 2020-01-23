FROM ubuntu:16.04
RUN apt-get update && \
	apt-get -y install openssh-server python && \
	echo 'root:root' |chpasswd && \
	sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config && \
	sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config && \
	mkdir /root/.ssh && \ 
	mkdir /var/run/sshd && \
	apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
EXPOSE 22

CMD    ["/usr/sbin/sshd", "-D"]
