FROM       ubuntu:16.04
MAINTAINER Rendo Wibawa rendo.aw@gmail.com

RUN apt-get update

RUN apt-get install -y openssh-server iproute2 inetutils-ping traceroute tcpdump tshark netcat
RUN mkdir /var/run/sshd

RUN echo 'root:root' |chpasswd

RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

EXPOSE 22

CMD    ["/usr/sbin/sshd", "-D"]
