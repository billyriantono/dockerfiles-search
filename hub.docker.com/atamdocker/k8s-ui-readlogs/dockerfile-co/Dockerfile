FROM ubuntu:16.04
WORKDIR /tmp
RUN apt-get -y update && \
    apt-get -y install git build-essential cmake libpng-dev libjpeg-dev libtiff-dev libxxf86vm1 libxxf86vm-dev libxi-dev libxrandr-dev graphviz && \
    apt-get -y clean && \
    git clone --recursive https://github.com/openMVG/openMVG.git && \
    cd openMVG && \
    git checkout -b v1.2 && \
    mkdir build && \
    cd build && \
    cmake -DCMAKE_BUILD_TYPE=RELEASE -DOpenMVG_BUILD_TESTS=ON -DOpenMVG_BUILD_EXAMPLES=ON . ../src/ && \
    make -j$(nproc) && \
    make install && \
    cd ../.. && \
    rm -rf /tmp/openMVG
ENTRYPOINT ["/bin/bash"]
