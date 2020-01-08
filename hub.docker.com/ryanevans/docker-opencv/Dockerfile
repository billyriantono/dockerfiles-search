FROM debian:sid

## Install build dependencies


WORKDIR /tmp

RUN apt-get -y update && apt-get -y install -qq wget unzip
RUN apt-get -y install -qq cmake libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev libboost-dev libboost-program-options-dev 

RUN 		wget -q "https://github.com/opencv/opencv/archive/3.2.0.zip" -O opencv.zip \
		&&	unzip -q opencv.zip \
		&&	mv opencv-3.2.0 opencv \
		&&	rm opencv.zip \
		&&	wget -q "https://github.com/opencv/opencv_contrib/archive/3.2.0.zip" -O opencv_contrib.zip \
		&&	unzip -q opencv_contrib.zip \
		&&	mv opencv_contrib-3.2.0 opencv_contrib \
		&&	rm opencv_contrib.zip \
		
		&& 	cd opencv \
		&& 	mkdir build \
		&& 	cd build \
		&&	cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local -D OPENCV_EXTRA_MODULES_PATH=/tmp/opencv_contrib/modules -D WITH_FFMPEG=ON -DWITH_LIBV4L=ON /tmp/opencv \
		&& 	make -j4 \
		&&	make install \
		&& 	rm -rf /tmp/
