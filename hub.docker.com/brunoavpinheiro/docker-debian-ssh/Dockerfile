FROM debian:latest

MAINTAINER Bruno Alberto da Veiga Pinheiro <contato@brunoavpinheiro.com.br>

RUN apt-get update -y && apt-get upgrade -y && apt-get install -y openssh-server && apt-get clean

RUN echo 'root:root' | chpasswd

RUN mkdir /var/run/sshd

RUN sed 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' -i /etc/ssh/sshd_config

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]