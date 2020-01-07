FROM nvidia/cuda:8.0-cudnn6-devel-ubuntu16.04

# Pick up some TF dependencies
RUN apt-get update -qq && apt-get install -y --no-install-recommends \
        build-essential \
        curl \
        libfreetype6-dev \
        libpng12-dev \
        libzmq3-dev \
        pkg-config \
        python3-dev \
        python3-tk \
        rsync \
        software-properties-common \
        unzip \
        && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install Conda
RUN curl -O https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/Anaconda3-4.2.0-Linux-x86_64.sh && \
    bash Anaconda3-4.2.0-Linux-x86_64.sh -b -p /opt/conda && \
    rm Anaconda3-4.2.0-Linux-x86_64.sh
ENV PATH=/opt/conda/bin:$PATH

# Conda Package
RUN rm /opt/conda/lib/icu/current && \
    conda install -y  hdfs3

RUN pip --no-cache-dir install \
        sklearn \
        opencv-python \
        tensorpack \
        && \
    python -m ipykernel.kernelspec

# Install TensorFlow GPU version.
RUN pip --no-cache-dir install tensorflow-gpu
# For CUDA profiling, TensorFlow requires CUPTI.
ENV LD_LIBRARY_PATH /usr/local/cuda/extras/CUPTI/lib64:$LD_LIBRARY_PATH
# Set up our notebook config.
COPY etc/jupyter_notebook_config.py /root/.jupyter/
# We just add a little wrapper script.
COPY etc/run_jupyter.sh /
# TensorBoard
EXPOSE 6006
# IPython
EXPOSE 8888
CMD ["bash run_jupyter.sh", "--allow-root"]

#TF High-level API
RUN pip --no-cache-dir install \
        keras \
        tflearn \
        tensorlayer \
        python_speech_features
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
