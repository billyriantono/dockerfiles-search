FROM ubuntu:16.04
LABEL maintainer "Alexey Umnov <alexeyum@gmail.com>"


RUN echo "deb http://archive.ubuntu.com/ubuntu trusty-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    apt-get -qq update && \
    apt-get install -y cmake \
                       wget \
                       unzip \
                       git \
                       zlib1g-dev \
                       libjpeg-dev \
                       libav-tools \
                       xorg-dev \
                       swig3.0 \
                       python-dev \
                       python3-dev \
                       python-pip \
                       python3-pip \
                       libopenblas-dev \
                       liblapack-dev \
                       libsdl2-dev \
                       libboost-all-dev \
                       gcc \
                       g++ && \
    ln -s /usr/bin/swig3.0 /usr/bin/swig

RUN pip install --upgrade pip \
                           scipy \
                           numpy && \
    pip install --upgrade sklearn \
                           jupyter \
                           tqdm \
                           matplotlib \
                           seaborn && \
    pip install --upgrade tensorflow \
                           http://download.pytorch.org/whl/cu80/torch-0.3.0.post4-cp27-cp27mu-linux_x86_64.whl \
                           torchvision \
                           keras     

RUN pip3 install --upgrade pip \
                           scipy \
                           numpy && \
    pip3 install --upgrade sklearn \
                           jupyter \
                           tqdm \
                           matplotlib \
                           seaborn && \
    pip3 install --upgrade http://download.pytorch.org/whl/cu80/torch-0.3.0.post4-cp35-cp35m-linux_x86_64.whl \
                           torchvision \
                           tensorflow \
                           keras && \                           
    python3 -m ipykernel.kernelspec


EXPOSE 8888
VOLUME /notebooks
WORKDIR /notebooks

COPY run_jupyter.sh /
CMD ["/run_jupyter.sh"]
