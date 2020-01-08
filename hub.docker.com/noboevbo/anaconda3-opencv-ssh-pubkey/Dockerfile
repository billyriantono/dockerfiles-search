FROM       continuumio/anaconda3:latest
MAINTAINER Dennis Ludl "https://github.com/noboevbo/machine-learning-docker"

RUN apt-get update

RUN conda install -c menpo opencv 

RUN apt-get install -y openssh-server
RUN apt-get install -y sudo #For automated pip installs via PyCharm
RUN echo 'root:root' |chpasswd

RUN mkdir /var/run/sshd

#ENV Variables for SSH access
RUN echo "export PATH=${PATH}" >> /root/.bashrc

#SSHD Config
RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config
RUN sed -i 's|[#]*PasswordAuthentication yes|PasswordAuthentication no|g' /etc/ssh/sshd_config
RUN mkdir /root/.ssh
RUN service ssh restart


EXPOSE 22

CMD    ["/usr/sbin/sshd", "-D"]