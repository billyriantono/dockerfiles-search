FROM ubuntu:14.04

RUN apt-get update
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd

RUN wget https://raw.githubusercontent.com/Azure-App-Service/node/master/6.11.0/sshd_config && mv /etc/ssh/sshd_config /etc/ssh/sshd_config.bak && cp sshd_config /etc/ssh/sshd_config

RUN bash -c 'echo "root:Docker!" | chpasswd'

EXPOSE 2222

CMD /usr/sbin/sshd -D