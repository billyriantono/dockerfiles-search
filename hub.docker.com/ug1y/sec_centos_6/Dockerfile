From i386/centos:6

MAINTAINER ug1y yinhao746746@163.com

RUN yum install -y openssh openssh-clients openssh-server telnet telnet-server zsh
RUN yum install -y gcc gdb vim iptstate system-config-firewall wireshark squid
RUN yum install -y openssl-* httpd-* mod_ssl

RUN echo password | passwd --stdin root
RUN useradd -m student
RUN echo password | passwd --stdin student
RUN useradd -m instructor
RUN echo password | passwd --stdin instructor

RUN service sshd start

CMD /bin/bash