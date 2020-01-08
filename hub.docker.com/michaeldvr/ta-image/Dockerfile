# Build using generator from https://github.com/ufoym/deepo
# ==================================================================
# module list
# ------------------------------------------------------------------
# python        3.6    (apt)
# tensorflow    1.5    (pip)
# ==================================================================

FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04
LABEL maintainer="Michael Devara <michael.devara@gmail.com>"
LABEL description="Tensorflow 1.5 GPU Python 3.6 on Ubuntu 16.04"

RUN APT_INSTALL="apt-get install -y --no-install-recommends" && \
    PIP_INSTALL="python -m pip --no-cache-dir install --upgrade" && \
    GIT_CLONE="git clone --depth 10" && \
    rm -rf /var/lib/apt/lists/* \
           /etc/apt/sources.list.d/cuda.list \
           /etc/apt/sources.list.d/nvidia-ml.list && \
    apt-get update && \
# ==================================================================
# tools
# ------------------------------------------------------------------
    DEBIAN_FRONTEND=noninteractive $APT_INSTALL \
        build-essential \
        ca-certificates \
        cmake \
        wget \
        git \
        vim \
        && \
# ==================================================================
# python
# ------------------------------------------------------------------
    DEBIAN_FRONTEND=noninteractive $APT_INSTALL \
        software-properties-common \
        && \
    add-apt-repository ppa:deadsnakes/ppa && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive $APT_INSTALL \
        python3.6 \
        python3.6-dev \
        && \
    wget -O ~/get-pip.py \
        https://bootstrap.pypa.io/get-pip.py && \
    python3.6 ~/get-pip.py && \
    ln -s /usr/bin/python3.6 /usr/local/bin/python3 && \
    ln -s /usr/bin/python3.6 /usr/local/bin/python && \
    $PIP_INSTALL \
        setuptools \
        && \
    $PIP_INSTALL \
        ipython~=6.5 \
        matplotlib==2.2.3 \
        numpy==1.15.1 \
        scipy==1.0.0 \
        opencv-python~=3.4 \
        scikit-image==0.14.0 \
        scikit-learn==0.19.2 \
        jupyter==1.0.0 \
        && \
# ==================================================================
# tensorflow
# ------------------------------------------------------------------
    $PIP_INSTALL \
        tensorflow-gpu==1.5 \
        && \
# ==================================================================
# config & cleanup
# ------------------------------------------------------------------
    ldconfig && \
    apt-get clean && \
    apt-get autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/* ~/*
# ==================================================================
# virtualenv & test python
# ------------------------------------------------------------------
#    pip install virtualenvwrapper && \
#    cat "export WORKON_HOME=$HOME/.virtualenvs" >> ~/.bashrc && \
#    cat "export PROJECT_HOME=$HOME/Devel" >> ~/.bashrc && \
#    cat "source /usr/local/bin/virtualenvwrapper.sh" >> ~/.bashrc && \
#    source ~/.bashrc && \
#    mkvirtualenv temp && \
#    workon temp && \
# ==================================================================
# test python
# ------------------------------------------------------------------
#    python --version && \
#    pip freeze
RUN ln -s /usr/local/cuda/lib64/stubs/libcuda.so /usr/local/cuda/lib64/stubs/libcuda.so.1
RUN ln -s /usr/local/cuda/lib64/stubs/libcuda.so /usr/local/cuda/lib64/libcuda.so.1
COPY .bashrc /root/.bashrc
#RUN echo LD_LIBRARY_PATH=/usr/local/cuda/lib64/stubs/:$LD_LIBRARY_PATH >> ~/.bashrc
#RUN LD_LIBRARY_PATH=/usr/local/cuda/lib64/stubs/:$LD_LIBRARY_PATH python3 setup.py install 
#RUN rm /usr/local/cuda/lib64/stubs/libcuda.so.1

EXPOSE 8888 6006
# CMD ["/bin/sh"]