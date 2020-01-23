FROM       ubuntu:16.04
MAINTAINER Jonathan Meyer "http://github.com/gisjedi"

RUN apt-get update

RUN apt-get install -y openssh-server sudo
RUN mkdir /var/run/sshd

RUN sed -ri 's/^#PasswordAuthentication\s+.*/PasswordAuthentication no/' /etc/ssh/sshd_config \
	&& sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config \
	&& echo 'AllowTcpForwarding no' >> /etc/ssh/sshd_config \
	&& echo 'X11Forwarding no' >> /etc/ssh/sshd_config 

COPY key-inject-sshd /key-inject-sshd

RUN chmod +x /key-inject-sshd

EXPOSE 22

CMD    ["/key-inject-sshd"]
