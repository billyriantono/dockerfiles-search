FROM ubuntu:xenial

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get install -y sudo git python-pip python-dev \
                       build-essential ssh libssl-dev \
                       curl openssh-server rsync vim

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6 && \
    echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list && \
    apt-get update && \
    apt-get install -y mongodb-org
RUN mkdir -p /data/db

RUN apt-get update && \
    apt-get install -y openjdk-8-jdk maven

RUN apt-get install -y mysql-server

RUN curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash - && \
    sudo apt-get install -y nodejs

RUN mkdir /var/run/sshd
RUN sed -i 's/PermitEmptyPasswords no/PermitEmptyPasswords yes/' /etc/ssh/sshd_config && \
    sed -i 's/PubkeyAuthentication yes/PubkeyAuthentication no/' /etc/ssh/sshd_config && \
    sed -i 's/RSAAuthentication yes/RSAAuthentication no/' /etc/ssh/sshd_config && \
    sed -i 's/UsePAM yes/UsePAM no/' /etc/ssh/sshd_config
EXPOSE 22

RUN sudo curl -O https://storage.googleapis.com/golang/go1.8.linux-amd64.tar.gz
RUN tar -xvf go1.8.linux-amd64.tar.gz
RUN mv go /usr/local

RUN useradd -ms /bin/bash dev && adduser dev sudo
RUN echo "%sudo   ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
RUN passwd -d dev

USER dev
WORKDIR /home/dev
RUN mkdir /home/dev/.ssh
#COPY authorized_keys /home/dev/.ssh/
RUN echo "PATH=$PATH:/usr/local/go/bin:/home/dev/go/bin" >> .bashrc
#RUN echo "GOPATH=/home/dev/go" >> .profile

USER root
#RUN chown dev /home/dev/.ssh/authorized_keys
#RUN chgrp dev /home/dev/.ssh/authorized_keys
#RUN chmod 644 /home/dev/.ssh/authorized_keys
CMD ["/usr/sbin/sshd", "-D"]
