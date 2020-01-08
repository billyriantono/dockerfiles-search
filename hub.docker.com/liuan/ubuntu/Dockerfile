FROM ubuntu:14.04

RUN apt-get update

RUN apt-get install -y wget curl htop vim ssh nginx

RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/g' /etc/ssh/sshd_config

RUN sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config

RUN echo root:123456a? | chpasswd

RUN mkdir -p /opt/an/test

EXPOSE 22

EXPOSE 80

CMD ["/etc/init.d/ssh", "start", "-D"]

