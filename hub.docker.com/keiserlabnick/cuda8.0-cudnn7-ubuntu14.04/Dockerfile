# Start with cuDNN base image
FROM nvidia/cuda:8.0-cudnn7-runtime-ubuntu14.04
MAINTAINER Nick Mew <mew@keiserlab.org>

# Install git, wget, python-dev, pip, BLAS + LAPACK and other dependencies
RUN apt-get update && apt-get install -y \
  gfortran \
  git \
  wget \
  liblapack-dev \
  libopenblas-dev \
  python-dev \
  python-pip \
  python-nose \
  python-numpy \
  python-scipy

# Set CUDA_ROOT
ENV CUDA_ROOT /usr/local/cuda/bin

# Install CMake 3
RUN cd /root && wget https://cmake.org/files/v3.8/cmake-3.8.2.tar.gz && \
  tar -xf cmake-3.8.2.tar.gz && cd cmake-3.8.2 && \
  ./configure && \
  make -j "$(nproc)" && \
  make install



# Install Cython
RUN pip install --upgrade pip
RUN pip install --upgrade setuptools
RUN pip install Cython

# Clone libgpuarray repo and move into it
RUN cd /root && git clone https://github.com/Theano/libgpuarray.git && cd libgpuarray && \
# Make and move into build directory
  mkdir Build && cd Build && \
# CMake
  cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr && \
# Make
  make -j"$(nproc)" && \
  make install
# Install pygpu
RUN cd /root/libgpuarray && \
  python setup.py build_ext -L /usr/lib -I /usr/include && \
  python setup.py install


# Install jupyter
RUN pip install --upgrade pip
RUN pip install --upgrade six
RUN pip install --upgrade jupyter matplotlib seaborn h5py regex scikit-learn 



