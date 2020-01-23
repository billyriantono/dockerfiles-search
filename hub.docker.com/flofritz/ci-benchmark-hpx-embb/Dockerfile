FROM ubuntu:latest

RUN apt-get update && \
    apt-get install -y build-essential \
                        git  \
                        cmake  \
                        gcc \
                        python \
                        lshw \
			llvm-5.0 \
			llvm-5.0-tools \
                        clang-5.0 \
                        libtbb-dev \
			wget \
			openjdk-8-jdk \
                        unzip \
                        zip \
                        pkg-config \
			zlib1g-dev \
			libboost-all-dev \
			unzip \
			google-perftools \
			libgoogle-perftools-dev

RUN update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-5.0 100 && \
    update-alternatives --install /usr/bin/clang clang /usr/bin/clang-5.0 100 && \
    update-alternatives --install /usr/bin/llvm-cov llvm-cov /usr/bin/llvm-cov-5.0 100 && \
    update-alternatives --install /usr/bin/llvm-profdata llvm-profdata /usr/bin/llvm-profdata-5.0 100

RUN git clone -q https://github.com/google/googletest.git /googletest \
  && cd googletest \
  && git checkout tags/release-1.8.0 \
  && mkdir -p /googletest/build \
  && cd /googletest/build \
  && cmake .. && make && make install \
  && cd / && rm -rf /googletest


RUN git clone -q https://github.com/google/benchmark.git /benchmark \
  && cd benchmark \
  && git checkout tags/v1.3.0 \
  && mkdir -p /benchmark/build \
  && cd /benchmark/build \
  && cmake -DCMAKE_BUILD_TYPE=Release .. && make && make install \
  && cd / && rm -rf /benchmark


RUN wget https://github.com/siemens/embb/archive/v1.0.0.zip \
  && unzip v1.0.0.zip \
  && cd embb-1.0.0/ \
  && mkdir build \
  && cd build \
  && cmake .. \
  && cmake --build . --config Release \
  && cmake --build . --target install

RUN wget http://stellar.cct.lsu.edu/files/hpx_1.1.0.zip \
 && unzip hpx_1.1.0.zip \
 && cd hpx_1.1.0/build \
 && cmake .. \
 && make install -j8

