FROM      ubuntu:15.04
MAINTAINER Leon Sixt <docker@leon-sixt.de>

LABEL Description="Image with clang:3.6, gcc:4.9, cmake, qt5, boost:1.58.0, opencv:2.4 and caffe:master"

RUN apt-get update
RUN apt-get install --yes gcc g++ \
                          clang-3.6 clang-3.6++ \
                          cmake git ssh  wget \
                          qt5-default libqt5opengl5-dev \
                          libopencv-dev \
                          liblmdb-dev \
                          opencl-headers \
                          build-essential protobuf-compiler \
                          libprotoc-dev \
                          hdf5-tools \
                          libhdf5-serial-dev \
                          libsnappy1 \
                          libsnappy-dev \
                          libatlas-base-dev \
                          libgoogle-glog0 \
                          libgoogle-glog-dev \
                          libgflags-dev \
                          liblmdb-dev \
                          libleveldb-dev \
                          python-numpy \
                          libopenblas-base \
                          libopenblas-dev \
                          gfortran

# http://stackoverflow.com/questions/12689304/ctypes-error-libdc1394-error-failed-to-initialize-libdc1394
RUN ln /dev/null /dev/raw1394

RUN ln /usr/bin/clang-3.6 /usr/bin/clang
RUN ln /usr/bin/clang++-3.6 /usr/bin/clang++

RUN apt-get build-dep --yes libboost-dev
ADD http://downloads.sourceforge.net/project/boost/boost/1.58.0/boost_1_58_0.tar.gz?r=http%3A%2F%2Fwww.boost.org%2Fusers%2Fhistory%2Fversion_1_58_0.html&ts=1433603736&use_mirror=vorboss /tmp/boost_1_58_0.tar.gz
RUN cd /tmp \
 && tar -xf boost_1_58_0.tar.gz \
 && cd ./boost_1_58_0 \
 && ./bootstrap.sh --with-libraries=filesystem,program_options,system,serialization,thread,date_time --exec-prefix=/usr/local \
 && ./b2 \
 && ./b2 install

RUN git clone https://github.com/BVLC/caffe.git /opt/caffe \
 && mkdir -pv /opt/caffe/build \
 && (cd /opt/caffe/build \
     && cmake -DCMAKE_CXX_COMPILER=/usr/bin/c++ -DBLAS=open -DCPU_ONLY=ON -DCMAKE_BUILD_TYPE=Release .. \
     && make all \
     && make install)
