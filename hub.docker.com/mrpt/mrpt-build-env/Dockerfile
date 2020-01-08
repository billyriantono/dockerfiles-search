FROM ubuntu:bionic
ARG DEBIAN_FRONTEND=noninteractive
RUN \
	apt update && \
	apt-get install -y build-essential clang-6.0 gcc g++ pkg-config \
		cmake python3-pip git-core ccache libftdi-dev \
		zlib1g-dev libusb-1.0-0-dev libdc1394-22-dev \
		libjpeg-dev libopencv-dev libgtest-dev libeigen3-dev \
		libsuitesparse-dev libopenni2-dev libudev-dev \
		libboost-python-dev libpython3-dev python3-numpy \
		libwxgtk3.0-gtk3-dev freeglut3-dev libavformat-dev \
		libswscale-dev libassimp-dev qtbase5-dev \
		libqt5opengl5-dev curl rsync liboctomap-dev \
		lib3ds-dev libpcap-dev libfreenect-dev libyaml-cpp-dev \
		liblas-dev liblas-c-dev \
		libjsoncpp-dev libtinyxml2-dev \
		libxrandr-dev \
		libroscpp-dev librosbag-dev libstd-srvs-dev libcv-bridge-dev \
		libsensor-msgs-dev libtf2-msgs-dev libtf2-dev libnav-msgs-dev \
		libgeometry-msgs-dev libstereo-msgs-dev \
		clang-format
