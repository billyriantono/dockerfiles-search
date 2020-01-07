FROM nvidia/cuda:8.0-cudnn5-devel-ubuntu16.04

ENV CUDNN_PATH=/usr/lib/x86_64-linux-gnu/libcudnn.so.5

# Install git, apt-add-repository and dependencies for iTorch
RUN apt-get update && \
    apt-get install -y \
        software-properties-common \
        git \
        curl \
        libzmq3-dev \
        libssl-dev \
        python-zmq \
        sudo
 
# Install Conda
RUN curl -O https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/Anaconda3-4.2.0-Linux-x86_64.sh && \
    bash Anaconda3-4.2.0-Linux-x86_64.sh -b -p /opt/conda && \
    rm Anaconda3-4.2.0-Linux-x86_64.sh
ENV PATH=/opt/conda/bin:$PATH
   
RUN conda install -y jupyter

# Run Torch7 installation scripts 
RUN git clone https://github.com/torch/distro.git /opt/torch --recursive && \
    cd /opt/torch && \
    bash install-deps && \
    ./install.sh

ENV PATH=/opt/torch/install/bin:$PATH

# Install iTorch
RUN git clone https://github.com/facebook/iTorch.git /opt/iTorch && \
    cd /opt/iTorch && \
    luarocks make

# luarocks install
RUN git config --global url."https://".insteadOf git:// && \
    luarocks install \
        mnist

# Default command is to run the itorch-notebook
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--allow-root" ,"--no-browser"]
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