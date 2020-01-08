FROM ubuntu:16.04

# Dependency Components Install
RUN    apt-get update \
    && apt-get -y install git gcc make openssl libssl-dev libbz2-dev libreadline-dev libsqlite3-dev \
    && apt-get -y install aria2 curl bzip2 \
    && apt-get clean

# Install Pyenv
RUN    cd /usr/local \
    && git clone git://github.com/yyuu/pyenv.git ./pyenv \
    && mkdir -p ./pyenv/versions ./pyenv/shims

# Environment Settings
ENV PYENV_ROOT /usr/local/pyenv
ENV PATH ${PYENV_ROOT}/shims:${PYENV_ROOT}/bin:${PATH}

# install latest anaconda3
RUN    pyversion=anaconda3-5.0.1 \
    && pyenv install ${pyversion} \
    && pyenv rehash \
    && pyenv global ${pyversion}

# conda update
RUN    conda update conda \
    && conda update --all
