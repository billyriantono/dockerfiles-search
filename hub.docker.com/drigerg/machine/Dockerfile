FROM ubuntu:16.04

MAINTAINER Pradeep Kumar A.V. <pradeepkumar1025@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV LANG C.UTF-8
# RUN locale-gen "en_US.UTF-8" && dpkg-reconfigure locales

# System dependencies
RUN apt-get update && apt-get install -y \
    vim \
    git \
    curl \
    wget \
    nano \
    cmake \
    unzip \
    pkg-config \
    imagemagick \
    build-essential > /dev/null

RUN apt-get update && apt-get install -y \
    espeak \
    libasound-dev \
    portaudio19-dev \
    libportaudio2 \
    libportaudiocpp0

# Miniconda3
ENV PATH /opt/conda/bin:$PATH
ENV LB_LIBRARY_PATH /opt/conda/lib:$LB_LIBRARY_PATH
RUN curl -Ls https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -o /tmp/install-miniconda.sh && \
    /bin/bash /tmp/install-miniconda.sh -b -p /opt/conda && \
    conda update --all -y

# Basic dependencies
RUN conda install -y bzip2 glib readline mkl openblas numpy scipy hdf5 \
    pillow matplotlib cython pandas gensim protobuf \
    lmdb leveldb boost glog gflags
RUN pip install pydot_ng nnpack h5py scikit-learn scikit-image && \
    python -c 'import h5py;h5py.run_tests()'

# OpenCV

RUN apt-get install -y libgtk2.0-dev > /dev/null
RUN conda install -y -c menpo opencv3 && \
    python -c "import cv2;print(cv2.__version__)"

RUN ldconfig

# Jupyter
RUN pip install -q jupyter jupyterlab && \
    jupyter --version

# TensorFlow
RUN git clone --depth 1 https://github.com/tensorflow/tensorflow.git /usr/src/tensorflow && \
    pip install -q tensorflow
RUN pip install tflearn

# Tools
RUN pip install flask click pyyaml

# Adding The Machine
ADD etc/machine /etc/machine
ADD ./ /machine
RUN pip install --upgrade /machine/

WORKDIR "/tmp/working"

ENTRYPOINT ["/bin/bash"]