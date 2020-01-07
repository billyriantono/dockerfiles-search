FROM rusxg/ubuntu-cmake-ffmpeg

RUN \
	apt-get update && \
        apt-get -y install unzip libjpeg-dev libpng-dev libtiff-dev && \
	wget https://codeload.github.com/opencv/opencv/zip/3.3.0 && \
	unzip 3.3.0 && \
	wget https://github.com/opencv/opencv_contrib/archive/3.3.0.tar.gz && \
	tar -xvf 3.3.0.tar.gz && \
	mkdir build && cd build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE -D OPENCV_EXTRA_MODULES_PATH=../opencv_contrib-3.3.0/modules ../opencv-3.3.0 && \
    make && \
	make install && \
	cd .. && rm -rf opencv-3.3.0 && \
	rm -rf opencv_contrib-3.3.0 && \
	rm -rf build && \
	apt-get -y clean all && \
	rm -rf /var/lib/apt/lists/*



