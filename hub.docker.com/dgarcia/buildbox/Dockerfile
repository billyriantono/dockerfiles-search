FROM oraclelinux:7.4
RUN yum install -y wget curl
RUN cd /etc/yum.repos.d/  && wget http://yum.oracle.com/public-yum-ol7.repo 
RUN yum install -y make git docker
RUN curl https://storage.googleapis.com/kubernetes-helm/helm-v2.5.1-linux-amd64.tar.gz -o /tmp/helm.tgz && \
	tar xvfz  /tmp/helm.tgz -C /tmp && \
	chmod +x /tmp/linux-amd64/helm && \
	mv /tmp/linux-amd64/helm /usr/local/bin 
RUN curl https://storage.googleapis.com/kubernetes-release/release/v1.9.3/bin/linux/amd64/kubectl  -o /usr/local/bin/kubectl && \
	chmod +x  /usr/local/bin/kubectl && \
	mkdir -p /usr/local/src 

WORKDIR /usr/local/src

