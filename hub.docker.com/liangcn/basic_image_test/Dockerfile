FROM ubuntu:18.04
MAINTAINER Edward-liang "zhangliangaws@163.com"
RUN sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list
RUN apt-get update

RUN apt-get update && apt-get install -y --no-install-recommends \
        wget \
        vim \
        apt-utils \
        unzip

RUN wget --no-check-certificate  -P /tmp --quiet https://repo.continuum.io/archive/Anaconda3-4.3.1-Linux-x86_64.sh
RUN cd /tmp && mv Anaconda3-4.3.1-Linux-x86_64.sh anaconda.sh
RUN /bin/bash /tmp/anaconda.sh -b -p /opt/conda
RUN rm /tmp/anaconda.sh
RUN echo "export PATH=/opt/conda/bin:$PATH" >> ~/.bashrc
RUN rm /bin/sh && ln -s /bin/bash /bin/sh
RUN source ~/.bashrc
RUN apt-get update
RUN /opt/conda/bin/conda install -c conda-forge jupyterhub==0.8.1
EXPOSE 22 8000 8888
