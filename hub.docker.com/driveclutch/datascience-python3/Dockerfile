# Adapted from https://github.com/eip/docker-alpine-jupyter-notebook

FROM alpine:latest

MAINTAINER Sang Venkatraman <sang@driveclutch.com>

RUN apk update && \
    apk add --no-cache gfortran libgfortran python3 python3-dev bash && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade pip setuptools && \
    rm -r /root/.cache

RUN apk add libjpeg \
    zlib \
    zlib-dev \
    tiff \
    freetype \
    py-pillow \
    musl-dev \
    gfortran \
    gsl \
    mariadb-libs \
    libxft-dev \
    pkgconfig \
    pkgconf \
    tmux \
    curl \
    nano \
    vim \
    htop \
    man \
    unzip \
    wget \
    g++ \
    libgfortran \
    make 

RUN apk add build-base postgresql-dev libffi-dev #needed for sqlalchemy to be installed correctly
RUN ln -s /usr/include/locale.h /usr/include/xlocale.h #needed for numpy to be installed correctly

COPY libs/* /tmp/
RUN source /tmp/blas.sh
RUN source /tmp/lapack.sh

COPY pip_install_*.txt /tmp/
RUN BLAS=~/src/BLAS/libfblas.a LAPACK=~/src/lapack-3.5.0/liblapack.a pip3 install -r /tmp/pip_install_phase1.txt
RUN BLAS=~/src/BLAS/libfblas.a LAPACK=~/src/lapack-3.5.0/liblapack.a pip3 install -r /tmp/pip_install_phase2.txt

VOLUME /opt/notebooks
ENTRYPOINT /usr/bin/jupyter-notebook --no-browser --ip=0.0.0.0 --notebook-dir=/opt/notebooks
EXPOSE 8888
