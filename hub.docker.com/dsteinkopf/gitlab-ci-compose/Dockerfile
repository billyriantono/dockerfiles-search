FROM ubuntu

MAINTAINER Dirk Steinkopf "https://github.com/dsteinkopf"

RUN apt-get update && \
	apt-get -y dist-upgrade && \
	apt-get -y autoremove && \
	apt-get clean && \
	apt-get install -y \
		openssh-client \
		python-pip

# docker things:
RUN apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common

RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
	apt-key fingerprint 0EBFCD88

RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

RUN apt-get update && \
	apt-get install -y docker-ce

RUN pip install 'docker>=1.7.0' && \
	pip install 'docker-compose>=1.7.0'

RUN docker-compose --version
RUN docker --version
