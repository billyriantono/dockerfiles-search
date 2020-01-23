FROM ubuntu:14.04

MAINTAINER Dmitriy Romanov <rdvlip@gmail.com>

RUN apt-get update && apt-get upgrade -y && apt-get install -y openssh-server

RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config

RUN mkdir /root/.ssh
ADD authorized_keys /root/.ssh/
RUN chmod -R 600 /root/.ssh/

RUN mkdir /var/run/sshd

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

RUN apt-get install python3-pip -y

CMD bash