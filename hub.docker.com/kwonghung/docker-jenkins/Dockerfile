FROM jenkins/jenkins:lts
LABEL maintainer="kwonghung.yip@gmail.com"

SHELL ["/bin/bash","-c"] 

USER root

RUN apt-get update; \
    apt-get install -y \
        apt-transport-https \
        curl \
        software-properties-common; \
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -; \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable"; \
    apt-get update; \
    apt-get install -y docker-ce; \
    apt-get purge -y --auto-remove \
        apt-transport-https \
        software-properties-common; \
    apt-get clean;
    
COPY plugin-list.txt /usr/share/jenkins/ref/plugin-list.txt

RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugin-list.txt; \
    usermod -aG docker jenkins

USER jenkins

