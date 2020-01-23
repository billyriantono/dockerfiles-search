FROM ubuntu:xenial
MAINTAINER duzihaoeya

RUN apt-get update && \
    apt-get install -y apt-transport-https ca-certificates curl software-properties-common && \
    curl -fsSL https://apt.dockerproject.org/gpg | apt-key add - && \
    add-apt-repository "deb https://apt.dockerproject.org/repo/ ubuntu-$(lsb_release -cs) main" && \ 
    apt-get update && \
    apt-get -y install docker-engine

RUN echo "deb http://repos.mesosphere.io/ubuntu $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/mesosphere.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv E56151BF && \
    apt-get -y update && \
    apt-get -y install mesos && \
    apt-get clean && rm -rf /var/lib/apt/lists/*