FROM gcc:7

RUN apt-get update && apt-get install -y --no-install-recommends \
    wget unzip git libgsl-dev libboost-all-dev \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
RUN wget https://cmake.org/files/v3.10/cmake-3.10.2.tar.gz \
       && tar -xzf cmake-3.10.2.tar.gz \
       && rm -f cmake-3.10.2.tar.gz \
       && cd cmake-3.10.2 \
       && ./bootstrap --prefix=/usr \
       && make && make install \
       && cd .. && rm -rf cmake-3.10.2
RUN wget https://github.com/fmtlib/fmt/releases/download/4.1.0/fmt-4.1.0.zip \
       && unzip fmt-4.1.0.zip \
       && cd fmt-4.1.0 \
       && mkdir build \
       && cd build \
       && cmake .. -DCMAKE_INSTALL_PREFIX:PATH=/usr -DCMAKE_BUILD_TYPE=Release \
       && make && make install \
       && cd ../.. && rm -rf fmt-4.1.0
RUN wget https://github.com/gabime/spdlog/archive/v0.16.3.tar.gz \
       && tar -xzf v0.16.3.tar.gz \
       && cd spdlog* \
       && mkdir build \
       && cd build \
       && cmake .. -DCMAKE_INSTALL_PREFIX:PATH=/usr -DCMAKE_BUILD_TYPE=Release \
       && make && make install \
       && cd ../.. && rm -rf spdlog*

