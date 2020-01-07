FROM rust:1.31.0
RUN apt-get update && apt-get install -y \ 
    wget \
    build-essential \ 
    cmake \ 
    git \
    libc-dev \
	qt5-default \
	libssl-dev \
	pkg-config

# Install Open CV - Warning, this takes absolutely forever
RUN mkdir -p /opencv cd /opencv && \
    git clone --branch 2.4 https://github.com/opencv/opencv.git &&\
    cd opencv && \
    mkdir build && \ 
    cd build && \
    cmake \
    -DWITH_QT=ON \ 
    -DWITH_OPENGL=ON \ 
    -DFORCE_VTK=ON \
    -DWITH_TBB=ON \
    -DWITH_GDAL=ON \
    -DWITH_XINE=ON \
    -DBUILD_EXAMPLES=ON .. && \
    make -j4 && \
    make install && \ 
    ldconfig && \
    rm -r /opencv
