FROM openjdk:8-jdk

# configure the ansible PPA
RUN echo 'deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main' >> /etc/apt/sources.list \
 && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367 

# install ansible
RUN apt-get update && apt-get install -y \
    python-jinja2 \
    python-yaml \
    python-paramiko \
    python-httplib2 \
    python-crypto \
    sshpass \
    ansible \
    openssh-client \
    openssh-server \
 && apt-get -q autoremove \
 && apt-get -q clean \
 && rm -rf /var/lib/apt/lists/*

# create host file
RUN mkdir -p /etc/ansible \
 && echo 'localhost' > /etc/ansible/hosts

RUN groupadd -g 1000 jenkins \
 && useradd -m -d /home/jenkins -u 1000 -g 1000 -s /bin/bash jenkins \
 && echo "jenkins:jenkins" | chpasswd

RUN groupadd ansible \
 && useradd -m -d /home/ansible -g ansible -s /bin/bash ansible \
 && echo "ansible:ansible" | chpasswd

#create 
RUN mkdir -p /var/run/sshd

# Standard SSH port
EXPOSE 22

# Default command
CMD ["/usr/sbin/sshd", "-D"]





