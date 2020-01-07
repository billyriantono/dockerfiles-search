FROM rusxg/ubuntu14-cmake-ffmpeg

RUN \
	apt-get update && \
        apt-get -y install unzip libjpeg-dev libpng-dev libtiff-dev && \
	wget https://codeload.github.com/opencv/opencv/zip/3.1.0 && \
	unzip 3.1.0 && \
	cd opencv-3.1.0 && \
	mkdir build && cd build && \
        cmake -D CMAKE_BUILD_TYPE=RELEASE -D WITH_IPP=OFF .. && \
        make && \
	make install && \
	cd .. && rm -rf opencv-3.1.0 && \
	apt-get -y clean all && \
	rm -rf /var/lib/apt/lists/*



