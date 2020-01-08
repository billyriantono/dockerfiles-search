FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04
WORKDIR /tmp

# Init
RUN apt-get update

# TimeZone
RUN apt-get install -y tzdata
ENV TZ Asia/Tokyo

# Japanese
RUN apt-get install -y language-pack-ja-base language-pack-ja
ENV LANG ja_JP.UTF-8
ENV LC_ALL ja_JP.UTF-8

# Anaconda
RUN apt-get install -y wget bzip2 build-essential && \
    echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh -O conda.sh && \
    /bin/bash conda.sh -b -p /opt/conda && \
    rm conda.sh
ENV PATH /opt/conda/bin:$PATH

# JupyterLab
RUN conda install -y -c conda-forge jupyterlab && \
    mkdir /teamlab
ENV SHELL /bin/bash
    
# OpenCV
RUN conda install -y -c https://conda.binstar.org/menpo opencv3
    
# TensorFlow 1.5(=cuda9)
RUN pip install tensorflow-gpu==1.5.* && \
    pip install --upgrade numpy

# PyTorch
RUN conda install -y -c pytorch torchvision

# XGBoost
RUN apt-get install -y git && \
    git clone --recursive https://github.com/dmlc/xgboost && \
    cd xgboost && \
    make -j4 && \
    cd python-package && \
    python setup.py install && \
    cd ../.. && \
    rm -rf xgboost

# Settings
WORKDIR /teamlab
VOLUME /teamlab
EXPOSE 8888 6006 3000
CMD jupyter lab --ip=0.0.0.0 \
                --allow-root \
                --no-browser \
                --NotebookApp.token='' \
                --NotebookApp.notebook_dir='/teamlab' \
                --NotebookApp.iopub_data_rate_limit=1000000000
