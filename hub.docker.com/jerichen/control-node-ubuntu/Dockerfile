FROM ubuntu:18.04
MAINTAINER JeriChen<jeri.chen0110@gmail.com>

ENV TZ=Asia/Taipei

# install ansible
RUN apt-get update
RUN apt-get install -y tzdata
RUN apt-get install -y vim
RUN apt-get install -y software-properties-common
RUN apt-add-repository ppa:ansible/ansible
RUN apt-get update
RUN apt-get install -y ansible
RUN apt-get install -y openssh-server 
RUN apt-get install -y python sudo curl wget bash-completion openssl 
RUN apt-get clean

# Setting timezone
RUN echo "Asia/Taipei" > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata

# Setting the sshd.
RUN mkdir /var/run/sshd
RUN echo 'root:password' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

# Setting ssh private && public key.
RUN mkdir /root/.ssh

RUN wget https://raw.githubusercontent.com/jerichen/docker-ansible/master/docker/files/ssh/id_rsa \
      -O /tmp/id_rsa && \
      mv /tmp/id_rsa /root/.ssh/ 

RUN wget https://raw.githubusercontent.com/jerichen/docker-ansible/master/docker/files/ssh/id_rsa.pub \
      -O /tmp/id_rsa.pub && \
      mv /tmp/id_rsa.pub /root/.ssh/ 

RUN wget https://raw.githubusercontent.com/jerichen/docker-ansible/master/docker/files/ssh/id_rsa.pub \
      -O /tmp/authorized_keys && \
      mv /tmp/authorized_keys /root/.ssh/ 

RUN chown -R root:root /root/.ssh/ && \
      chmod 600 /root/.ssh/id_rsa && \
      chmod 600 /root/.ssh/id_rsa.pub && \
      chmod 644 /root/.ssh/authorized_keys && \
      chmod 700 /root/.ssh

# make dev
RUN mkdir /root/dev

# open port 22
EXPOSE 22

# Run ssh server daemon.
CMD ["/usr/sbin/sshd", "-D"]
