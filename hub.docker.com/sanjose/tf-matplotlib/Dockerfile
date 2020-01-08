FROM sanjose/centos7
MAINTAINER sanjose

RUN cd ~ \
    && yum install epel-release -y \
    && yum install python-pip -y \
    && pip install tensorflow \
    && yum install python-matplotlib -y \
    && pip install --upgrade pip \
    && /usr/bin/yes | pip uninstall numpy && pip install -U numpy \
    && python -c "import numpy as np; print np.__version__" \
    && yum upgrade -y \
    && yum clean all \
    && rm -rf ~/.cache/pip

WORKDIR /root/neural-network

COPY simple_neural_network.py /root/
