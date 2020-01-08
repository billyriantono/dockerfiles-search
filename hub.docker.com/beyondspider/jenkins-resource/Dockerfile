FROM beyondspider/curl:latest

MAINTAINER from www.beyondspider.com by admin (admin@beyondspider.com)

RUN mkdir -p /tmp/download && \
	curl -s -o /tmp/download/jenkins.war https://download.beyondspider.com/docker/jenkins-2.176.1.war && \
    curl -s -o /tmp/download/apache-maven-3.6.1-bin.tar.gz https://download.beyondspider.com/docker/apache-maven-3.6.1-bin.tar.gz && \
	curl -s -o /tmp/download/gradle-5.4.1-bin.zip https://download.beyondspider.com/docker/gradle-5.4.1-bin.zip && \
	curl -s -o /tmp/download/node-v10.16.0-linux-x64.tar.xz https://download.beyondspider.com/docker/node-v10.16.0-linux-x64.tar.xz && \
	curl -s -o /tmp/download/jenkins_home.tar.gz https://download.beyondspider.com/docker/jenkins_home.tar.gz
