FROM ubuntu:18.04

ARG THEANO_VERSION=1.0.0
ARG TENSORFLOW_VERSION=1.12.0
ARG TENSORFLOW_ARCH=cpu
ARG KERAS_VERSION=2.2.4
ARG LASAGNE_VERSION=0.2.dev1
ARG TORCH_VERSION=1.0.0
ARG CAFFE_VERSION=master
ARG PYTHON_VERSION=36
ENV DEBIAN_FRONTEND=noninteractive


# Install some dependencies
RUN apt-get update -qq && apt-get install -y -qq \
		bc \
		build-essential \
		cmake \
		curl \
		g++ \
		gfortran \
		git \
		libffi-dev \
		libfreetype6-dev \
		libhdf5-dev \
		liblcms2-dev \
		libopenblas-dev \
		liblapack-dev \
		libssl-dev \
		libtiff5-dev \
		libwebp-dev \
		libzmq3-dev \
		nano \
		pkg-config \
		software-properties-common \
		unzip \
		vim \
		wget \
		zlib1g-dev \
		qt5-default \
		libvtk6-dev \
		zlib1g-dev \
		libjpeg-dev \
		libwebp-dev \
		libpng-dev \
		libtiff5-dev \
		libopenexr-dev \
		libgdal-dev \
		libdc1394-22-dev \
		libavcodec-dev \
		libavformat-dev \
		libswscale-dev \
		libtheora-dev \
		libvorbis-dev \
		libxvidcore-dev \
		libx264-dev \
		yasm \
		libopencore-amrnb-dev \
		libopencore-amrwb-dev \
		libv4l-dev \
		libopenjp2-7-dev \
		libtbb-dev \
		libeigen3-dev \
		python3-dev \
		python3-tk \
		python3-numpy \
		python3-pip \
		ant \
		default-jdk \
		doxygen \
		&& \
	apt-get clean && \
	apt-get autoremove && \
	rm -rf /var/lib/apt/lists/*


# Add SNI support to Python
RUN pip3 --no-cache-dir install \
		pyopenssl \
		ndg-httpsclient \
		pyasn1

# Install other useful Python packages using pip
RUN pip3 --no-cache-dir install --upgrade ipython && \
	pip3 --no-cache-dir install \
		Cython \
		ipykernel \
		jupyter \
		path.py \
		Pillow \
		pygments \
		six \
		sphinx \
		wheel \
		zmq \
		&& \
	python3 -m ipykernel.kernelspec


# Install TensorFlow
RUN pip3 --no-cache-dir install \
	https://storage.googleapis.com/tensorflow/linux/${TENSORFLOW_ARCH}/tensorflow-${TENSORFLOW_VERSION}-cp${PYTHON_VERSION}-cp${PYTHON_VERSION}m-linux_x86_64.whl


RUN apt-get update -qq && apt-get install -qq caffe-cpu && \
	apt-get clean && \
	apt-get autoremove && \
	rm -rf /var/lib/apt/lists/*

RUN pip3 --no-cache-dir install git+git://github.com/Theano/Theano.git && \
	\
	echo "[global]\ndevice=cpu\nfloatX=float32\nmode=FAST_RUN \
		\n[lib]\ncnmem=0.95 \
		\n[nvcc]\nfastmath=True \
		\n[blas]\nldflag = -L/usr/lib/openblas-base -lopenblas \
		\n[DebugMode]\ncheck_finite=1" \
	> /root/.theanorc


# Install Keras
RUN pip3 --no-cache-dir install git+git://github.com/keras-team/keras.git


# Install Lasagne
RUN pip3 --no-cache-dir install git+git://github.com/Lasagne/Lasagne.git

# Install OpenCV
RUN apt-get update -qq && apt-get install python3-opencv -y -qq && \ 
	apt-get clean && \
	apt-get autoremove && \
	rm -rf /var/lib/apt/lists/* && \
	rm -rf /tmp/*

RUN pip3 install --no-cache-dir scikit-learn \
	numpy \
	scipy \
	matplotlib \
	pandas \
	sympy \
	nose \
	scikit-image \
	h5py

RUN pip3 install --no-cache-dir https://download.pytorch.org/whl/cpu/torch-1.0.0-cp36-cp36m-linux_x86_64.whl  \
	torchvision


# Set up notebook config
COPY jupyter_notebook_config.py /root/.jupyter/

# Jupyter has issues with being run directly: https://github.com/ipython/ipython/issues/7062
COPY run_jupyter.sh /root/
RUN chmod 777 /root/run_jupyter.sh

# Expose Ports for TensorBoard (6006), Ipython (8888)
EXPOSE 6006 8888

WORKDIR "/root"
CMD ["/bin/bash"]
