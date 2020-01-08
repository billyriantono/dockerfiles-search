FROM jenkins:latest

USER root
RUN echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" >> /etc/apt/sources.list &&\
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367 &&\
    apt-get update && \
    apt-get -y install ansible python-pip rsync && \
    pip install aliyuncli aliyun-python-sdk-slb aliyun-python-sdk-ecs && \
    rm -rf /var/lib/apt/lists/*
