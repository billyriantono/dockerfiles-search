FROM ubuntu:14.04

RUN apt-get update && apt-get install -y \
git \
python2.7 \
python-pip \
python-numpy \
python-scipy \
libhdf5-dev


#install h5py
RUN pip install Cython
RUN pip install h5py

#install pyyaml
RUN pip install pyyaml

RUN pip install git+git://github.com/Theano/Theano.git
RUN cd / && git clone https://github.com/fchollet/keras.git && cd keras && python2.7 setup.py install