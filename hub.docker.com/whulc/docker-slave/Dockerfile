FROM ubuntu
MAINTAINER calos Liu <whulc@outlook.com>

RUN apt-get update
RUN apt-get -y upgrade
#RUN apt-get -y install \
#	linux-image-extra-$(uname -r) \
#	linux-image-extra-virtual
RUN apt-get -y install \
	apt-transport-https \
	ca-certificates \
	curl \
	software-properties-common
RUN curl -fsSL \
	https://download.docker.com/linux/ubuntu/gpg | apt-key add -
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
RUN apt-get update
RUN apt-get install -y docker-ce
