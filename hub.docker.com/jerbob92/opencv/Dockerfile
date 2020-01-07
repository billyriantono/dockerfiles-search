from	ubuntu:14.04

# Ubuntu sides with libav, I side with ffmpeg.
run	echo "deb http://ppa.launchpad.net/mc3man/gstffmpeg-keep/ubuntu trusty main" >> /etc/apt/sources.list
run	apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 90BD7EACED8E640A 
run	apt-get update
run	apt-get install -y -q wget curl
run	apt-get install -y -q build-essential
run	apt-get install -y -q cmake
run     apt-get install -y -q python3 python3-dev python3-pip python3-setuptools
run	pip3 install numpy
run	apt-get install -y -q libavformat-dev libavcodec-dev libavfilter-dev libswscale-dev
run	apt-get install -y -q libjpeg-dev libpng-dev libtiff-dev libjasper-dev zlib1g-dev libopenexr-dev libxine-dev libeigen3-dev libtbb-dev
run     apt-get install -y -q libopencv-dev build-essential cmake git libgtk2.0-dev pkg-config python-dev python-numpy libdc1394-22 libdc1394-22-dev libjpeg-dev libpng12-dev libtiff4-dev libjasper-dev libavcodec-dev libavformat-dev libswscale-dev libxine-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libv4l-dev libtbb-dev libqt4-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev x264 v4l-utils unzip default-jre default-jdk ant
add	build_opencv.sh	/build_opencv.sh
run	/bin/sh /build_opencv.sh
run	rm -rf /build_opencv.sh
run     apt-get -y -q install maven2
run     apt-get -y -q install libtesseract-dev
run     wget https://tesseract-ocr.googlecode.com/files/tesseract-ocr-3.02.eng.tar.gz && tar xvfz tesseract-ocr-3.02.eng.tar.gz && mv tesseract-ocr/tessdata /usr/local/share/tessdata && rm tesseract-ocr-3.02.eng.tar.gz && rm -R tesseract-ocr
