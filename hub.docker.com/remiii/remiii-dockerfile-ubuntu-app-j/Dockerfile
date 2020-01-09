############################################################
# Dockerfile to build JekyllApp container images
# Based on Ubuntu
# Author Remi Barbe (aka Remiii)
############################################################

# Set the base image to Ubuntu
FROM ubuntu:12.04

# File Author / Maintainer
MAINTAINER Remi Barbe (aka Remiii)

# Env
ENV MYPASSWORD root

# Update
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
RUN apt-get update
RUN apt-get upgrade -y

# set root password
RUN echo "root:$MYPASSWORD" > /root/passwdfile
RUN cat /root/passwdfile | chpasswd

#################### BEGIN INSTALLATION ####################
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y vim htop curl zsh htop build-essential ruby1.9.1 ruby1.9.1-dev gems git-core ntp tig tmux screen wget openssh-server supervisor
RUN gem update
RUN gem install jekyll
RUN sudo useradd -m -d /home/website -s /bin/bash website
RUN sudo usermod -G sudo -a website
RUN sudo usermod -G adm -a website
RUN sudo chown website:website /home/website
ADD ./skel/ /
#################### INSTALLATION END ######################

# After
EXPOSE 22 4000
CMD ["/usr/bin/supervisord", "-n"]

