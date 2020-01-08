#based on rastasheep/ubuntu-sshd
FROM  ubuntu:latest

WORKDIR /root
COPY shx.bash /root
RUN chmod +x /root/shx.bash

ENV ROOT_PASSWORD dockerssh

RUN \
	apt-get update && \
	apt-get install -y p7zip-full curl openssh-server && \
	mkdir /var/run/sshd

RUN echo "root:${ROOT_PASSWORD}" |chpasswd

RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

RUN mkdir /root/.ssh

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 22
EXPOSE 17000-17999

CMD    ["/usr/sbin/sshd", "-D"]

