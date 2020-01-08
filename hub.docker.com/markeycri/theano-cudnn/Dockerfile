FROM nvidia/cuda:9.2-cudnn7-devel-ubuntu16.04

RUN apt-get update && apt-get install -y \
	vim \
	wget \
	cmake \
	python-numpy \
	python-scipy \
	python-dev \
	python-pip \
	python-nose \
	g++ \
	libopenblas-dev \
	git \
	libblas3 \
	liblapack3 \
	liblapack-dev \
	libblas-dev \
	gfortran

RUN pip install Theano sklearn gensim cython

RUN git clone https://github.com/Theano/libgpuarray.git ~/libgpuarray

RUN mkdir ~/libgpuarray/Build && cd ~/libgpuarray/Build && cmake .. -DCMAKE_BUILD_TYPE=Release && make && make install

RUN cd ~/libgpuarray && python setup.py build && python setup.py install && ldconfig

WORKDIR "/root"
CMD ["/bin/bash"]
