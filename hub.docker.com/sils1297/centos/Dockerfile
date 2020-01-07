FROM centos:centos7
MAINTAINER Lasse Schuirmann lasse.schuirmann@gmail.com

RUN yum update -y
RUN yum install zsh vim wget hostname -y
RUN usermod -s /bin/zsh root
RUN sed -i 's,/bin/bash,/bin/zsh,' /etc/default/useradd
RUN wget -O /etc/zshrc http://git.grml.org/f/grml-etc-core/etc/zsh/zshrc
