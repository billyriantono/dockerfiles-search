# Dockerfile for baseline machine learning development
# * Ubuntu 16.04.2 
# * Tensorflow 1.3 GPU w/ Python2
# * Theano
# * scikit-learn
# * numpy
# * matplotlib
# * pandas
# * keras 

FROM gcr.io/tensorflow/tensorflow:latest-devel-gpu
MAINTAINER Cetin Mericli cetin.mericli@gmail.com

# setup environment
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y --fix-missing --no-install-recommends \
	apt-utils \
	locales \
	module-init-tools \
	binutils \
	dbus \
	wget \
	vim \
	screen \
	nano \
	git \
	mercurial \
	bash-completion \
	ipython \
	aptitude \
	htop \
	mesa-utils \
	mlocate \
	gdb \
	locate \
	htop \
	linux-tools-common \
	usbutils \
	xterm \
	iperf \
	google-perftools \
	python-imaging \	
	libhdf5-dev \ 
	graphviz \
	mc \
    && apt-get dist-upgrade -y \
	&& rm -rf /var/lib/apt/lists/* 


RUN updatedb

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8


# let's have colored shell prompt
RUN sed -i -- 's/#force_color_prompt=yes/force_color_prompt=yes/g' ~/.bashrc
RUN echo "export QT_GRAPHICSSYSTEM=native" >> ~/.bashrc

# Conda

ENV CONDA_DIR /opt/conda
ENV PATH $CONDA_DIR/bin:$PATH

RUN mkdir -p $CONDA_DIR && \
	echo export PATH=$CONDA_DIR/bin:'$PATH' > /etc/profile.d/conda.sh && \
	wget --quiet https://repo.continuum.io/miniconda/Miniconda3-4.2.12-Linux-x86_64.sh && \
	echo "c59b3dd3cad550ac7596e0d599b91e75d88826db132e4146030ef471bb434e9a *Miniconda3-4.2.12-Linux-x86_64.sh" | sha256sum -c - && \
	/bin/bash ./Miniconda3-4.2.12-Linux-x86_64.sh -f -b -p $CONDA_DIR && \
	rm Miniconda3-4.2.12-Linux-x86_64.sh

# Python
ARG python_version=2.7

RUN conda install -y python=${python_version} && \
	pip install --upgrade pip && \
	pip install tensorflow-gpu && \
	conda install Pillow scikit-learn notebook pandas matplotlib mkl nose pyyaml six h5py && \
	conda install theano pygpu spyder && \
	git clone https://github.com/fchollet/keras.git && pip install -e ./keras[tests] && \
	pip install git+https://github.com/fchollet/keras.git && \
	pip install keras-vis && \
	pip install pydot && \
	pip install commentjson && \
	conda clean -yt

ENV PYTHONPATH='/src/:$PYTHONPATH'
ENV USER=root
ENV HOME=/root

ADD theanorc ${HOME}/.theanorc
ADD spyder.ini ${HOME}/.config/spyder/spyder.ini
RUN cp -f /var/lib/dbus/machine-id /etc/machine-id

# add custom vimrc and screenrc files for convenience
ADD vimrc ${HOME}/.vimrc
ADD screenrc ${HOME}/.screenrc


