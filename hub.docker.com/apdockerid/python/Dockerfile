FROM apdockerid/build_tools:latest
LABEL maintainer="Andreas Pettersson"
ARG BUILD_PATH=home/build
RUN  mkdir -p ${BUILD_PATH}

# Install dependencies needed to build python
RUN apt-get update && apt-get install -y \
    openssl \
    libssl-dev \
    zlib1g-dev \
    libbz2-dev \
    libffi-dev \
 && rm -rf /var/lib/apt/lists/*

# Build and install python
ARG BUILD_PATH_PYTHON=${BUILD_PATH}/cpython
ARG PYTHON_VERSION=v3.7.5rc1
RUN  git -C ${BUILD_PATH} clone https://github.com/python/cpython.git
RUN  git -C ${BUILD_PATH_PYTHON} checkout tags/${PYTHON_VERSION}
RUN ["bin/bash","-c", "cd ${BUILD_PATH_PYTHON}; ./configure --enable-optimizations --with-lto; make -j$(nproc); make install; ldconfig /usr/local/lib"]
RUN rm -r ${BUILD_PATH}

# Upgrade pip to latest version
RUN pip3 install --upgrade pip