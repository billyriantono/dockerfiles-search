FROM ubuntu:18.04
LABEL maintainer="gissler@fifty2.eu"

RUN apt-get update && apt-get install -y clang wget make && \
    rm -rf /var/lib/apt/lists/*

# Define which compiler we want to use.
ENV CC=/usr/bin/clang
ENV CXX=/usr/bin/clang

# Download and install latest cmake.
RUN mkdir -p /tmp/cmake_download && \
    cd /tmp/cmake_download && \
    wget -nv 'https://github.com/Kitware/CMake/releases/download/v3.13.4/cmake-3.13.4-Linux-x86_64.sh' && \
    bash cmake-3.13.4-Linux-x86_64.sh --prefix=/usr/local --exclude-subdir && \
    cd && \
    rm -rf /tmp/cmake_download

# Download and install mpi.
RUN export current_dir=$pwd && \
    mkdir ${current_dir}/mpich-3.2-install && \
    mkdir -p /tmp/mpi_download && \
    cd /tmp/mpi_download && \
    wget -nv 'http://www.mpich.org/static/downloads/3.2/mpich-3.2.tar.gz' && \
    tar -xzf mpich-3.2.tar.gz && \
    mkdir mpich-3.2-build && \
    cd mpich-3.2-build/ && \
    ../mpich-3.2/configure -prefix=${current_dir}/mpich-3.2-install --disable-fortran --disable-cxx && \
    make -s && \
    make install && \
    cd && \
    rm -rf /tmp/mpi_download
# Update the path such that mpi is found.
ENV PATH="/mpich-3.2-install/bin:${PATH}"

# Download and install Python 3.5.
RUN apt-get update && apt-get install -y software-properties-common && \
    wget https://bootstrap.pypa.io/get-pip.py -O /tmp/get-pip.py && \
    add-apt-repository ppa:deadsnakes/ppa && \
    apt-get update && \
    apt-get install -y python3.5-dev && \
    python3.5 /tmp/get-pip.py && \
    rm -rf /tmp/
# Install pip packages for Python 3.5.
RUN python3.5 -m pip install six progressbar2 wheel

# Download and install Python 2.7.
RUN mkdir -p /tmp && wget https://bootstrap.pypa.io/get-pip.py -O /tmp/get-pip.py && \
    apt-get update && \
    apt-get install -y python2.7-dev && \
    python2.7 /tmp/get-pip.py && \
    rm -rf /tmp/
# Install pip packages for Python 2.7.
RUN python2.7 -m pip install wheel

# Download and install Qt 5.7.
ADD qt-installer-noninteractive.qs /tmp/qt_download/script.qs
RUN apt-get update && apt-get install -y libgl1-mesa-dev fontconfig && \
    mkdir -p /tmp/qt_download && \
    cd /tmp/qt_download && \
    wget -nv 'http://download.qt.io/archive/qt/5.7/5.7.1/qt-opensource-linux-x64-5.7.1.run' && \
    chmod +x ./qt-opensource-linux-x64-5.7.1.run && \
    ./qt-opensource-linux-x64-5.7.1.run --script ./script.qs -platform minimal && \
    cd && \
    rm -rf /tmp/qt_download && \
    rm -rf /var/lib/apt/lists/*
