FROM caffe2ai/caffe2:c2v0.8.1.cuda8.cudnn7.ubuntu16.04

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