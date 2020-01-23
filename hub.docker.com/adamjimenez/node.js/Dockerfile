FROM ubuntu:14.04
MAINTAINER Adam Jimenez <adam.jimenez@gmail.com>

#RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
RUN apt-get update
RUN apt-get upgrade -y

#might need this
#RUN export DEBIAN_FRONTEND=noninteractive

RUN apt-get install -y openssh-server supervisor nodejs npm nano git

RUN mkdir -p /var/run/sshd
RUN mkdir -p /var/log/supervisor

RUN useradd ubuntu -d /home/ubuntu -m -U
RUN chown -R ubuntu:ubuntu /home/ubuntu
#RUN sudo adduser ubuntu sudo
#RUN echo ubuntu:ubuntu | chpasswd
RUN echo 'ubuntu ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers.d/ubuntu
RUN chmod 0440 /etc/sudoers.d/ubuntu

RUN mkdir -p /home/ubuntu/workspace
ADD bashrc /home/ubuntu/.bashrc
ADD default_readme.md /home/ubuntu/workspace/README.md
ADD default_index.html /home/ubuntu/workspace/index.html
RUN chown -R ubuntu:ubuntu /home/ubuntu

RUN mkdir -p /home/ubuntu/.ssh
RUN chown ubuntu:ubuntu /home/ubuntu/.ssh
RUN chmod 700 /home/ubuntu/.ssh

#RUN sed -ri 's/^PermitRootLogin.*$/PermitRootLogin yes/g' /etc/ssh/sshd_config

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD run /usr/local/bin/
RUN chmod +x /usr/local/bin/run

# Define mountable directories.
VOLUME ["/home/ubuntu/workspace"]

CMD ["/usr/local/bin/run"]
EXPOSE 80 22
