FROM ubuntu:latest
RUN apt-get update
RUN apt-get -y install openssh-server ansible vim
RUN mkdir -p /etc/ansible/group_vars
RUN mkdir -p /root/.ssh; chmod 700 /root/.ssh
RUN mkdir -p /root/.keys; chmod 700 /root/.keys
RUN ssh-keygen -t rsa -N "" -f /root/.ssh/id_rsa
RUN sed -i 's/#PubkeyAuthentication/PubkeyAuthentication/g' /etc/ssh/sshd_config
RUN sed -i 's/#PermitRootLogin/PermitRootLogin/g' /etc/ssh/sshd_config 
COPY hosts /etc/ansible/hosts
