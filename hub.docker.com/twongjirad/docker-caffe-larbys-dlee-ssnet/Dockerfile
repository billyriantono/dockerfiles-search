FROM twongjirad/docker-deps-caffe-larbys

MAINTAINER taritree.wongjirad@tufts.edu

RUN mkdir -p /usr/local/larbys/ && \
    cd /usr/local/larbys && \
    apt-get -y update && \
    apt-get -y install libprotobuf-dev libboost-all-dev libgoogle-glog-dev libopenblas-dev libgflags-dev \
      protobuf-compiler libhdf5-dev libleveldb-dev liblmdb-dev libsnappy-dev python-protobuf python-skimage && \
    git clone https://github.com/LArbys/ssnet_example && \
    cd ssnet_example && git checkout tmw_container && cp larbys.sh /etc/ && \
    cd sw && chmod +x setup.sh && ls -lh && \
    bash -c "source setup.sh" && \
    apt-get autoremove -y && apt-get clean -y