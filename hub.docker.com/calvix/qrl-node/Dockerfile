FROM fedora:latest

RUN dnf -y install \
	python3-devel \
	python3-pip \
	cmake \
	openssl-devel \
	libffi-devel \
	gcc \
	gcc-c++ \
	swig \
        git \
	hwloc-devel \
        boost-devel && \
    pip3 install -U setuptools && \
    pip3 install -U qrl && \
    dnf clean all -y && \
    git clone -b v0.62 https://github.com/theQRL/QRL qrl && \
    cd qrl && \
    pip3 install -r requirements.txt && \
    mkdir -p /root/.qrl
    
ADD ./config.yml /root/.qrl/config.yml
ADD ./entrypoint.sh /entrypoint.sh

ENTRYPOINT /entrypoint.sh
