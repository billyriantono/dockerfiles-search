FROM jasonalexanderlh/docker-opencv34-cuda101:latest
MAINTAINER Jason Alexander "jason.alexander.lh@hotmail.com"

#       %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
#       %     Why's the rhum always gone?      %
#       %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
#       %                                      %
#       %                @@@@@(                %
#       %             @@@@@@@@@@@/             %
#       %           .@&@@@@@@@@@@@/            %
#       %           @@@@@@@@@@@@@@@            %
#       %           #/@   %@%   @@@            %
#       %             @   @#@   @              %
#       %            @@@@@@ @@@@@@             %
#       %               @@@@@@@                %
#       %     @@@      @ @@@,. @       @#      %
#       %  /@@@@@@     @@/@@@ @@     %@%.@*    %
#       %  @@@& *@@@@   .@@@@@     @@@@@@@@@   %
#       %        .@@@@@@@     *@@@@@@@@@/      %
#       %             #@@@@@ @@@@              %
#       %             @@@/&@@@@@               %
#       %  @@@@@@@@@@@@@      @@@@@@@@#,       %
#       %   %@@@@@@%              @@@@@@@@@    %
#       %     @@(                   .@.%*      %
#       %                                      %
#       %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

###
#  Boost Library for OIIO
###

RUN apt-get update && apt-get install -y \
        libboost-all-dev \
###
#  OSSIM
###
# OSSIM Dependencies
        libtiff5-dev \
        libopenthreads-dev \
        libjpeg-dev \
        libgeos++-dev \
        libgeotiff-dev \
        libcurl4-openssl-dev \
        libsqlite3-dev \
        libproj-dev && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Charls
RUN wget https://github.com/team-charls/charls/archive/1.0.tar.gz && tar -xzf 1.0.tar.gz
WORKDIR "/charls-1.0"
RUN sed -i.bak 's/.*add_executable/#&/; s/.*target_link_libraries/#&/' /charls-1.0/CMakeLists.txt
RUN cmake . -DCMAKE_INSTALL_PREFIX=/opt -Dcharls_BUILD_SHARED_LIBS=ON -DCMAKE_CXX_FLAGS="-O2" -DCMAKE_C_FLAGS="-O2" && make -j8 && \
mkdir -p /charls-1.0/charls-build/include/CharLS && mkdir -p /charls-1.0/charls-build/lib && \
cp *.h /charls-1.0/charls-build/include/CharLS && cp libCharLS.so /charls-1.0/charls-build/lib/ && cd /charls-1.0/charls-build && cp -r ./* /usr && \
cd / && rm -r /charls-1.0 && rm /1.0.tar.gz

RUN apt-get update && apt-get install -y \
    libsuitesparse-dev \
    libfreeimage-dev \
    libgflags-dev \
    libglew-dev \
    freeglut3-dev \
    libjpeg-dev \
    libceres-dev \
#    liblas-dev \
#    liblas-c-dev \
    libgtk2.0-dev \
    pkg-config \
    libavcodec-dev \
    libavformat-dev \
    libswscale-dev \
    libtbb2 \
    libtbb-dev \
    libjpeg-dev \
    libpng-dev \
    libtiff-dev \
    libboost-all-dev \
    coinor-libcbc-dev \
    coinor-libclp-dev \
    librapidxml-dev \
    ffmpeg \
    ## Cleanup
    && apt-get clean && rm -rf /var/lib/apt/lists/*

###
#  OpenEXR
###

# Build and install OpenEXR
RUN mkdir -p /openexr && \
    mkdir -p /openexr/build && \
    cd /openexr && \
    wget https://github.com/openexr/openexr/archive/master.zip && \
    unzip master.zip

RUN cd /openexr/build && \
        cmake ../openexr-master  \
            -DCMAKE_BUILD_TYPE=Release \
            -DCMAKE_INSTALL_PREFIX:PATH=/usr \
            -DCMAKE_CXX_STANDARD=17 \
            -DCMAKE_CXX_STANDARD_REQUIRED=ON \
            -DCMAKE_CXX_EXTENSIONS=OFF \
            -DCMAKE_CXX_FLAGS="-std=c++17" \
            -DOPENEXR_BUILD_ILMBASE=ON \
            -DOPENEXR_BUILD_OPENEXR=ON \
            -DOPENEXR_BUILD_PYTHON_LIBS=OFF \
            -DOPENEXR_BUILD_TESTS=OFF && \
        make -j7 && \
        make install && \
# Cleanup OpenEXR
    cd / && \
    rm -r /openexr
###! End OpenEXR Block !###


###
#  fmt
###
RUN mkdir -p /fmt && \
    mkdir -p /fmt/build && \
    cd /fmt && \
    wget https://github.com/fmtlib/fmt/archive/5.3.0.zip && \
    unzip 5.3.0.zip

RUN cd /fmt/build && \
    cmake ../fmt-5.3.0  \
        -DCMAKE_BUILD_TYPE=Release && \
    make -j7 && \
    make install && \
# Cleanup fmt
    rm -r /fmt
###! End fmt Block !###


###
#  rapidJSON
###

# Build and install rapidJSON

RUN mkdir -p /rapidjson && \
    mkdir -p /rapidjson/build && \
    cd /rapidjson && \
    wget https://github.com/Tencent/rapidjson/archive/master.zip && \
    unzip master.zip

RUN cd /rapidjson/build && \
    cmake ../rapidjson-master \
        -DCMAKE_BUILD_TYPE=Release \
        -DCMAKE_CXX_FLAGS="-std=c++17" && \
    make -j7 && \
    make install && \
# Cleanup rapidJSON
    rm -r /rapidjson
###! End rapidJSON Block !###


###
#  ROCKSdb
###

#RUN apt-get update && apt-get install -y \
#    libsnappy-dev \
#    zlib1g-dev \
#    libbz2-dev \
#    libzstd-dev \
#    librocksdb5.8 \
#    librocksdb-dev \
#    ## Cleanup
#    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Build and install ROCKSdb

RUN mkdir -p /rocksdb && \
    mkdir -p /rocksdb/build && \
    cd /rocksdb && \
    wget https://github.com/facebook/rocksdb/archive/6.2.fb.zip && \
    unzip 6.2.fb.zip

RUN cd /rocksdb/build && \
    cmake ../rocksdb-6.2.fb \
        -DCMAKE_BUILD_TYPE=Release \
        -DWITH_TESTS=OFF \
        -DWITH_TOOLS=OFF \
        -DCMAKE_CXX_FLAGS="-std=c++17" && \
    make all -j4 && \
    make install && \
# Cleanup rocksdb
    rm -r /rocksdb
###! End rocksdb Block !###