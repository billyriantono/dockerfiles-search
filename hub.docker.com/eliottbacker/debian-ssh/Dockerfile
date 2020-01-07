FROM debian:jessie

MAINTAINER Eliott BACKER "eliott.backer@gmail.com"

# no question/dialog is asked during apt-get install
ENV DEBIAN_FRONTEND noninteractive

# update 
RUN apt-get -qq update

# Install some basic tools needed for deployment
RUN apt-get install -yqq wget curl nano git

# install ssh server
RUN apt-get install -yqq openssh-server

# change root password
RUN echo 'root:eliott' | chpasswd

# set authentication mode & enable PAM
RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
    
# Cleanup some things.
RUN apt-get autoremove -y
RUN apt-get clean 
RUN rm -rf /var/lib/apt/lists

RUN mkdir -p /var/run/sshd

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
