FROM gcr.io/cloud-solutions-images/jenkins-k8s-slave:v4
ENV DOCKER_VERSION 17.06.0~ce-0~debian

RUN apt-get update && \
	apt-get install -y \
	software-properties-common \
	apt-transport-https \
	ca-certificates \
	curl \
	gnupg2

RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -

RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"

RUN apt-get update && \
	apt-get install -y docker-ce=${DOCKER_VERSION}
