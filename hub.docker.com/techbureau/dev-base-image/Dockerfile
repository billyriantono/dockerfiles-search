FROM alpine:3.9
MAINTAINER Catapult Development Team
RUN apk update && apk add \
    ccache \
    cmake \
    curl \
    g++ \
    git \
    make \
    linux-headers \
    xz \
    gdb \
    ninja \
    python3 \
    su-exec 
RUN curl -o boost_1_69_0.tar.gz -SL https://dl.bintray.com/boostorg/release/1.69.0/source/boost_1_69_0.tar.gz && \
    tar -xzf boost_1_69_0.tar.gz && \
    cd boost_1_69_0 && \
    ./bootstrap.sh  && \
    ./b2 stage release && \
    ./b2 install  || \
    ./b2 install || echo "force rebuild 1" && \
    cd .. && rm -rf boost_1_69_0 boost_1_69_0.tar.gz
RUN git clone https://github.com/google/googletest.git && \
    cd googletest && \
    git checkout release-1.8.1 && \
    mkdir _build && cd _build && \
    cmake -DCMAKE_CXX_FLAGS='' -DCMAKE_BUILD_TYPE=Release -DCMAKE_POSITION_INDEPENDENT_CODE=ON .. && \
    make && make install && \
    cd ../.. && \
    rm -rf googletest && echo "force gtest rebuild 1"
RUN git clone https://github.com/google/benchmark.git && \
    cd benchmark && \
    git checkout v1.4.1 && \
    mkdir _build && cd _build && \
    cmake -DCMAKE_CXX_FLAGS='' -DCMAKE_BUILD_TYPE=Release -DBENCHMARK_ENABLE_GTEST_TESTS=OFF .. && \
    make && make install && \
    cd ../.. && \
    rm -rf benchmark
RUN git clone https://github.com/mongodb/mongo-c-driver.git && \
    cd mongo-c-driver && \
    git checkout 1.13.0 && \
    mkdir _build && cd _build && \
    cmake -DENABLE_AUTOMATIC_INIT_AND_CLEANUP=OFF -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local .. && \
    make && make install && \
    cd ../.. && \
    rm -rf mongo-c-driver
RUN git clone https://github.com/mongodb/mongo-cxx-driver.git && \
    cd mongo-cxx-driver && \
    git checkout r3.4.0 && \
    sed -i "s/, count/, static_cast<int64_t>(count)/" src/mongocxx/options/change_stream.cpp && \
    grep count src/mongocxx/options/change_stream.cpp && \
    mkdir _build && cd _build && \
    cmake -DCMAKE_CXX_FLAGS='' -DBOOST_ROOT=/usr/local -DBSONCXX_POLY_USE_BOOST=1 -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local .. && \
    make && make install && \
    cd ../.. && \
    rm -rf mongo-cxx-driver 
RUN git clone git://github.com/zeromq/libzmq.git && \
    cd libzmq && \
    git checkout master && \
    mkdir _build && cd _build  && \
    cmake -DCMAKE_CXX_FLAGS='' -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local .. && \
    make && make install && \
    cd ../.. && \
    rm -rf libzmq
RUN git clone https://github.com/zeromq/cppzmq.git && \
    cd cppzmq && mkdir _build && cd _build && \
    cmake -DCMAKE_CXX_FLAGS='' -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local .. && \
    make && make install && \
    cd ../.. && \
    rm -rf cppzmq
RUN curl -o gflags-2.2.2.tar.gz -SL https://github.com/gflags/gflags/archive/v2.2.2.tar.gz && \
    tar -xzf gflags-2.2.2.tar.gz && \
    cd gflags-2.2.2 && \
    mkdir _build && cd _build && \
    cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local -DBUILD_SHARED_LIBS=ON .. && \
    make && make install && \
    cd ../.. && \
    rm -rf gflags-2.2.2 gflags-2.2.2.tar.gz
RUN git clone https://github.com/facebook/rocksdb.git && \
    cd rocksdb && \
    git checkout origin/5.18.fb && \
    mkdir _build && cd _build && \
    cmake -DCMAKE_BUILD_TYPE=Release -DWITH_TESTS=OFF -DCMAKE_INSTALL_PREFIX=/usr/local .. && \
    make && make install && \
    cd ../.. && \
    rm -rf rocksdb
RUN apk add python3-dev && \
    pip3 install --upgrade pip setuptools && \
    pip install ply pylint pycodestyle
RUN echo "docker image build "
CMD ["/bin/ash"]
