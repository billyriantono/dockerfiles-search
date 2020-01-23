FROM openjdk:8-jdk-alpine

ENV container docker
ENV HOME /opt
ENV ENV="/opt/.profile"

ENV HELM_VERSION=2.13.0
ENV KUBECTL_VERSION=1.11.8
ENV KOPS_VERSION=1.11.1
ENV MAVEN_VERSION=3.6.0
ENV TERRAFORM_VERSION=0.11.11

WORKDIR /opt
USER root

RUN apk --no-cache add shadow && \
	apk --no-cache add curl nmap-ncat bash sudo git docker python3 jq openssh openssl && \
	rm -rf /var/lib/apt/lists/* && \
	curl https://storage.googleapis.com/kubernetes-release/release/v$KUBECTL_VERSION/bin/linux/amd64/kubectl > /usr/local/bin/kubectl && \
	chmod +x /usr/local/bin/kubectl && \
	curl -LO https://storage.googleapis.com/kubernetes-helm/helm-v$HELM_VERSION\-linux-amd64.tar.gz && \
	tar -zxvf helm-v$HELM_VERSION\-linux-amd64.tar.gz && \
	mv linux-amd64/helm /usr/local/bin/helm && \
	chmod +x /usr/local/bin/helm && \
	rm -rf linux-amd64 && \
	rm helm-v$HELM_VERSION\-linux-amd64.tar.gz && \
    pip3 install --upgrade pip setuptools && \
	pip3 install awscli && \
	curl -L https://github.com/kubernetes/kops/releases/download/$KOPS_VERSION/kops-linux-amd64 > /usr/local/bin/kops && \
	chmod +x /usr/local/bin/kops && \
	wget http://apache.mirrors.ionfish.org/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION\-bin.tar.gz && \
	tar xzvf apache-maven-$MAVEN_VERSION\-bin.tar.gz && \
	rm apache-maven-$MAVEN_VERSION\-bin.tar.gz && \
    curl -LO https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
	unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
	mv terraform /usr/local/bin/terraform && \
	rm -rf linux-amd64 && \
	chmod -R 777 /opt && \
   	ln -s /opt/apache-maven-$MAVEN_VERSION/bin/mvn /usr/local/bin/mvn && \
   	ln -s /opt/.local/bin/aws /usr/local/bin/aws
