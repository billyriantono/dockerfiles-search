From fedora:26

MAINTAINER ug1y yinhao746746@163.com

RUN dnf install -y openssh openssh-clients telnet zsh gcc gdb iputils
RUN dnf install -y mlocate john vim nmap hping3 wireshark authconfig
RUN dnf install -y file which findutils passwd man net-tools procps-ng
RUN dnf install -y hostname

RUN echo password | passwd --stdin root
RUN useradd -m student
RUN echo password | passwd --stdin student
RUN useradd -m instructor
RUN echo password | passwd --stdin instructor

CMD /bin/bash