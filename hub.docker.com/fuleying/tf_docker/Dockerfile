# Dockerfile for Doc AI environment.

ARG TF_VERSION=1.12.0-py3

FROM tensorflow/tensorflow:${TF_VERSION}

LABEL maintainer "Lambert <lambert.fu@oocl.com>"

ENV REFRESHED_AT 2019-01-03

# Install basic dependencies
RUN apt-get -yqq update && apt-get install -qqy --no-install-recommends \
        htop \
        tmux \
        vim \
        curl \
        git-core \
        && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

COPY .bashrc /root/

# install Anaconda3
RUN curl -O https://repo.continuum.io/archive/Anaconda3-2018.12-Linux-x86_64.sh \
    && bash Anaconda3-2018.12-Linux-x86_64.sh -b \
    && rm Anaconda3-2018.12-Linux-x86_64.sh

ENV PATH /root/anaconda3/bin:$PATH

# Configure Anaconda3 environment
RUN conda create -n jupyter pip python=3.6.6 \
    && echo "source activate jupyter" >> ~/.bashrc

ENV PATH /root/anaconda3/envs/jupyter/bin:$PATH

RUN pip --no-cache-dir install -q \
        ipython \
        pandas \
        jupyter \
        matplotlib \
        jupyter_contrib_nbextensions \
        jupyter_nbextensions_configurator \
        jupyterthemes \
        autopep8 \
        && \
    pip --no-cache-dir install -q --upgrade jupyterthemes && \
    pip uninstall -y notebook && \
    pip --no-cache-dir install -q notebook==5.6.0 && \
    jupyter contrib nbextension install --user && \
    jupyter nbextensions_configurator enable --user

COPY .jupyter /root/.jupyter/

# SHELL ["/bin/bash", "-c", "source /root/.bashrc"]

# jupyter notebok port
EXPOSE 8888

# build packages from source
WORKDIR /notebooks
# WORKDIR /tf
# VOLUME ["/tf"]

# Set default command when executing the container
# ENTRYPOINT ["/bin/bash", "-c"]
# CMD []

CMD ["/bin/sh", "-c", "which python && jupyter notebook --allow-root"]
