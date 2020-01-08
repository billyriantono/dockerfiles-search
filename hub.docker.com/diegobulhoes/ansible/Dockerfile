FROM diegobulhoes/docker-ssh-keygen:latest

ARG PASSWORD_ROOT=passwordRoot
ARG PASSWORD_USER_SSH=passwordUserSSH
ARG NEW_PASSPHRASE=newPassphrase

USER app
RUN yes y | ssh-keygen -q  -f /home/app/.ssh/id_rsa -N '${NEW_PASSPHRASE}'

USER root
RUN yes y | ssh-keygen -q  -f /root/.ssh/id_rsa -N '${NEW_PASSPHRASE}'

RUN apt update && apt install -y software-properties-common && \
    apt-add-repository --yes ppa:ansible/ansible && \
    apt update && apt install ansible -y && \
    rm -rf /var/lib/apt/list/*

RUN echo "app:""${PASSWORD_USER_SSH}" | chpasswd
RUN echo "root:""${PASSWORD_ROOT}" | chpasswd

RUN sed -i 's/#AuthorizedKeysFile.*2/AuthorizedKeysFile .ssh\/workers\/AuthorizedKeysFile .ssh\/master\/AuthorizedKeysFile/' /etc/ssh/sshd_config 

RUN mkdir -p /home/app/.ssh/workers/ && \
    cat /home/app/.ssh/id_rsa.pub > /home/app/.ssh/workers/AuthorizedKeysFile

RUN mkdir -p /root/.ssh/master/ && \
    cat /root/.ssh/id_rsa.pub > /root/.ssh/master/AuthorizedKeysFile 
