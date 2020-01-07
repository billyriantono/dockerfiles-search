FROM ubuntu:xenial

MAINTAINER godleon@gmail.com

RUN apt-get update && apt-get install -y software-properties-common

RUN add-apt-repository cloud-archive:ocata -y

RUN apt-get update && apt-get install -y \
    python2.7 \
    python-pip \
    curl \
    git-core \
    python-dev \
    libffi-dev \
    libssl-dev \
    python3-openstackclient \
    python3-heatclient \
    python3-swiftclient
    
RUN pip install --upgrade pip


RUN git clone https://github.com/openstack/tempest.git

WORKDIR /
RUN pip install tempest/

CMD ["/bin/bash"]