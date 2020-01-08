FROM maven:3.6-jdk-8

MAINTAINER Maximilian Schmitt

RUN apt-get update \
	&& apt-get install -y jq python-pip curl apt-transport-https \
	&& apt-get clean \
	&& pip install awscli

RUN curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
RUN echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list
RUN apt-get update && apt-get install -y kubectl && apt-get clean
RUN mkdir /root/.kube
