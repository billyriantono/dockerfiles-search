FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04

MAINTAINER kterao@slac.stanford.edu

ENV CUDA_DEVICE_ORDER=PCI_BUS_ID
ENV ROOTSYS=/usr/local/root
ENV PATH="${ROOTSYS}/bin:${PATH}"
ENV LD_LIBRARY_PATH="${ROOTSYS}/lib:${LD_LIBRARY_PATH}"
ENV PYTHONPATH="${ROOTSYS}/lib:${PYTHONPATH}"

RUN apt-get -y update
RUN apt-get -y install zsh dpkg-dev g++ gcc binutils libqt4-dev git wget emacs vim openssh-client && \
    apt-get -y install python-dev python-tk python-pip python-qt4 python-setuptools libsparsehash-dev python3-setuptools libhdf5-dev

# asciinema
RUN apt-get install -y locales && \
    locale-gen en_US.UTF-8 && \
    apt-get -y install software-properties-common python-software-properties && \
    apt-add-repository -y ppa:zanchey/asciinema && \
    apt-get -y update && \
    apt-get -y install asciinema

# ROOT
RUN wget https://root.cern.ch/download/root_v6.14.04.Linux-ubuntu16-x86_64-gcc5.4.tar.gz && \
    tar -xzf root_v6.14.04.Linux-ubuntu16-x86_64-gcc5.4.tar.gz && \
    rm root_v6.14.04.Linux-ubuntu16-x86_64-gcc5.4.tar.gz && \
    mv root /usr/local/root && \
    export ROOTSYS=/usr/local/root && \
    export PATH=${ROOTSYS}/bin:${PATH} && \
    export LD_LIBRARY_PATH=${ROOTSYS}/lib:${LD_LIBRARY_PATH} && \
    export PYTHONPATH=${ROOTSYS}/lib:${PYTHONPATH}

# pip basics
RUN pip --no-cache-dir --disable-pip-version-check install --upgrade pip==9.0.3 && \
    pip --no-cache-dir --disable-pip-version-check install --upgrade setuptools && \
    pip --no-cache-dir --disable-pip-version-check install 'matplotlib<3.0' && \
    pip --no-cache-dir --disable-pip-version-check install 'ipython<6.0'    && \
    pip --no-cache-dir --disable-pip-version-check install 'ipykernel<5.0'  && \
    pip --no-cache-dir --disable-pip-version-check install future numpy wheel zmq six pygments pyyaml cython gputil psutil humanize && \
    pip --no-cache-dir --disable-pip-version-check install h5py tqdm scipy seaborn tables root_numpy && \
    pip --no-cache-dir --disable-pip-version-check install pandas scikit-image scikit-learn Pillow opencv-python && \
    pip --no-cache-dir --disable-pip-version-check install jupyter notebook && \
    pip --no-cache-dir --disable-pip-version-check install plotly cufflinks && \
    pip --no-cache-dir --disable-pip-version-check install osfclient



