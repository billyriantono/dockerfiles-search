FROM jenkins/jnlp-slave:latest

USER root
RUN apt-get update \
      && apt-get upgrade -y \
      && apt-get install -yq sudo \
	apt-transport-https \
    	ca-certificates \
   	curl \
    	gnupg-agent \
    	software-properties-common \
      && rm -rf /var/lib/apt/lists/*

RUN curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
RUN apt-key fingerprint 0EBFCD88
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
RUN apt-get update && apt-get install -yq docker-ce docker-ce-cli containerd.io

RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers

USER jenkins
