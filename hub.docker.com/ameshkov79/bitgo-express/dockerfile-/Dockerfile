# deeplearning base image
FROM centos
MAINTAINER allocator

# version control
ENV DL_BASE_VERSION_CTL 14/6/2018 11:10:00

# set env
ENV ANACONDA_HOME /usr/local/anaconda3

# install basic software vim
RUN yum install -y vim

# install anaconda3 py3.5.x
RUN yum install -y wget
RUN yum install -y bzip2
RUN mkdir -p /home/download
RUN cd /home/download
RUN wget https://repo.continuum.io/archive/Anaconda3-4.2.0-Linux-x86_64.sh
RUN chmod 755 ./Anaconda3-4.2.0-Linux-x86_64.sh
RUN ./Anaconda3-4.2.0-Linux-x86_64.sh -b -p /usr/local/anaconda3
RUN rm -rf /home/download/*

# create link
RUN ln -s $ANACONDA_HOME/bin/python /usr/bin/python3
RUN ln -s $ANACONDA_HOME/bin/pip /usr/bin/pip3
RUN ln -s $ANACONDA_HOME/bin/conda /usr/bin/conda

# install tensorflow with cpu
RUN pip3 install --upgrade --ignore-installed tensorflow

# install keras 
RUN conda install -y keras
