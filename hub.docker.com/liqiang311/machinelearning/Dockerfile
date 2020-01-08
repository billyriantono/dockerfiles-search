FROM ubuntu:16.04

RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        curl \
        libfreetype6-dev \
        libpng12-dev \
        libzmq3-dev \
        pkg-config \
        python-dev \
        python-tk \
        rsync \
        software-properties-common \
        unzip \
        && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install Conda
RUN curl -O https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/Anaconda2-4.2.0-Linux-x86_64.sh && \
    bash Anaconda2-4.2.0-Linux-x86_64.sh -b -p /opt/conda && \
    rm Anaconda2-4.2.0-Linux-x86_64.sh
ENV PATH=/opt/conda/bin:$PATH

RUN conda install -y gensim

RUN pip --no-cache-dir install \
        tensorflow \
        keras \
        tflearn \
        tensorlayer \
        python_speech_features \
        sklearn \
        opencv-python \
        tensorpack
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