FROM bvlc/caffe:gpu

ENV CAFFE_VERSION 0.15

RUN echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64 /" > /etc/apt/sources.list.d/nvidia-ml.list && \
    apt-get update -qq && apt-get install -y --no-install-recommends \
        caffe-nv \
        caffe-nv-tools \
        python-caffe-nv \
        libcaffe-nv0 \
    && rm -rf /var/lib/apt/lists/* && \
    rm /etc/apt/sources.list.d/nvidia-ml.list

RUN apt-get update -qq && \
    apt-get install -y --no-install-recommends \
        ipython \
        ipython-notebook \
        python-sklearn \
        python-skimage \
        python-protobuf \
    && rm -rf /var/lib/apt/lists/*
#custom-tail
RUN apt-get update -qq && \
    apt-get install -y -qq \
        openssh-server \
        vim \
        nano \
        git \
        subversion \
        dos2unix \
        tzdata \
    && rm -rf /var/lib/apt/lists/*

RUN sed -i 's/^PermitRootLogin.*$/PermitRootLogin yes/g' /etc/ssh/sshd_config
RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo 'Asia/Shanghai' > /etc/timezone 
RUN env > /etc/environment

COPY etc/sources-tuna-ubuntu16.list /etc/apt/sources.list
COPY etc/pip-tuna.conf /root/.pip/pip.conf
COPY etc/condarc /root/.condarc