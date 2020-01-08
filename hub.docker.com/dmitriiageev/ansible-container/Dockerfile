FROM dmitriiageev/ansible:latest
MAINTAINER Dmitrii Ageev <d.ageev@gmail.com>

# Install auxiliary software packages
USER root
RUN apt update
RUN apt install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    python-pip

# Add Docker's official GPG key
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -

# Add Docker's repository
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

# Install Docker CE
RUN apt update
RUN apt install -y docker-ce
RUN gpasswd -a developer docker

# Install Ansible-Container
RUN pip install --upgrade pip
RUN pip install ansible-container[docker,k8s]

# Run a software piece as non-root user
USER $UNAME
WORKDIR $HOME/ansible
CMD /bin/bash
