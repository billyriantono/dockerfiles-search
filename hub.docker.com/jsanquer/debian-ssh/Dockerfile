FROM debian:testing

MAINTAINER Jean-Marc Sanquer <jean-marc@sanquer.com>

RUN apt-get update -y && apt-get upgrade -y

RUN apt-get install -y openssh-server \
 && mkdir /var/run/sshd \
 && chmod 0755 /var/run/sshd \
 && sed -i -e "s/\#PasswordAuthentication.*/PasswordAuthentication\ no/" /etc/ssh/sshd_config \
 && mkdir /root/.ssh \
 && touch /root/.ssh/authorized_keys \
 && chmod 700 /root/.ssh/authorized_keys \
 && chmod -R 700 /root/.ssh

ENTRYPOINT echo $SSH_KEY | base64 -d >/root/.ssh/authorized_keys && /usr/sbin/sshd 

CMD /bin/bash 

EXPOSE 22

