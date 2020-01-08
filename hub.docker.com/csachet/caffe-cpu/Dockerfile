FROM debian:jessie

ENV DEBIAN_FRONTEND noninteractive
ENV PATH $PATH:/opt/caffe/bin
ENV PYTHONPATH /opt/caffe/python

RUN echo 'deb http://ftp.debian.org/debian jessie main' > /etc/apt/sources.list \
&& echo 'deb http://ftp.debian.org/debian jessie-updates main' >> /etc/apt/sources.list \
&& echo 'deb http://security.debian.org jessie/updates main' >> /etc/apt/sources.list \
&& apt-get update && apt-get -y upgrade && apt-get -y install --no-install-recommends \
libprotobuf-dev libprotobuf-lite9 \
libleveldb-dev libleveldb1 \
libsnappy-dev libsnappy1 \
libopencv-dev libopencv-highgui2.4 libopencv-imgproc2.4 libopencv-core2.4 \
libhdf5-serial-dev \
protobuf-compiler \
\
libboost-all-dev libboost-system1.55.0 libboost-thread1.55.0 libboost-filesystem1.55.0 libboost-python1.55.0 \
\
libatlas-base-dev libatlas3-base \
\
python-dev libpython2.7 \
\
libgflags-dev libgflags2 \
libgoogle-glog-dev libgoogle-glog0 \
liblmdb-dev liblmdb0 \
\
cython \
python-numpy \
python-scipy \
python-skimage \
python-matplotlib \
python-h5py \
python-networkx \
python-nose \
python-pandas \
python-protobuf \
python-pil \
python-six \
\
wget \
bsdtar \
cmake \
python-pip \
build-essential \
\
\
&& wget https://github.com/BVLC/caffe/archive/rc3.zip -qO- | bsdtar -xvf- -C /usr/src \
&& cd /usr/src/caffe-rc3 \
&& pip install -r python/requirements.txt \
&& mkdir -p build && cd build \
&& cmake -DCMAKE_INSTALL_PREFIX=/opt/caffe -DCPU_ONLY=1 ../ \
&& make all \
&& make runtest \
&& make install \
&& cd \
&& rm -rf /usr/src/caffe-rc3 \
\
\
&& apt-get -y remove --purge \
wget bsdtar cmake build-essential \
libgflags-dev libgoogle-glog-dev liblmdb-dev \
python-dev \
libatlas-base-dev \
libboost-all-dev \
libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler \
&& apt-get -y autoremove --purge \
&& apt-get clean \
&& apt-get autoclean \
&& rm -rf /var/lib/apt/lists/* \
&& ln /dev/null /dev/raw1394
