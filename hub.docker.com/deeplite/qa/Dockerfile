FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04
MAINTAINER Deeplite (info@deeplite.ai)

# Packages needed for pyenv
RUN apt-get update && apt-get install -y --no-install-recommends \
            dh-autoreconf git curl \
            build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev \
            libsqlite3-dev wget llvm libncurses5-dev xz-utils tk-dev \
            libxml2-dev libxmlsec1-dev libffi-dev openjdk-8-jdk curl \
            bash-completion unzip python python-pip python-setuptools

WORKDIR /
RUN git clone https://github.com/pyenv/pyenv.git /pyenv
ENV PYENV_ROOT /pyenv
ENV PATH $PYENV_ROOT/bin:$PATH
RUN echo 'eval "$(pyenv init -)"' >> ~/.bashrc

RUN pyenv install 2.7.16
RUN pyenv install 3.5.5
RUN pyenv install 3.6.5
RUN pyenv install 3.7.3

RUN pyenv local 2.7.16
