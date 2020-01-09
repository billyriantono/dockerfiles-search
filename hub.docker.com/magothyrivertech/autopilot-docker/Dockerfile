FROM ubuntu:latest
MAINTAINER Christopher Cannell <Chris@MagothyRiverTech.com>

ENV APP_PATH=/usr/local
WORKDIR $APP_PATH

# install dependencies
RUN apt-get update -y && \
	apt-get install -y python3-pip wget unzip build-essential git pkg-config xxd && \
	pip3 install conan && \
	wget https://cmake.org/files/v3.13/cmake-3.13.2-Linux-x86_64.tar.gz && \
	wget https://github.com/ninja-build/ninja/releases/download/v1.8.2/ninja-linux.zip && \
	tar xf cmake-3.13.2-Linux-x86_64.tar.gz && \
	unzip ninja-linux.zip && \
	mv ninja cmake-3.13.2-Linux-x86_64/bin/ && \
	rm cmake-3.13.2-Linux-x86_64.tar.gz ninja-linux.zip

# 64c9750f53b0d049a4cd9ec771bc1dc397a9fb65 is core-moos master as of 2018/12/14
RUN git clone https://github.com/themoos/core-moos.git core-moos-src && \
	(cd core-moos-src && \
	 git checkout 64c9750f53b0d049a4cd9ec771bc1dc397a9fb65) && \
	mkdir -p core-moos-build && \
	/usr/local/cmake-3.13.2-Linux-x86_64/bin/cmake \
		-S core-moos-src -B core-moos-build \
		-DCMAKE_BUILD_TYPE=Debug \
		-DCMAKE_INSTALL_PREFIX=/usr/local/core-moos \
		-DCMAKE_EXPORT_NO_PACKAGE_REGISTRY=1 \
		-DCMAKE_FIND_PACKAGE_NO_PACKAGE_REGISTRY=1 \
		-DCMAKE_FIND_PACKAGE_NO_SYSTEM_PACKAGE_REGISTRY=1 \
		-DBUILD_SHARED_LIBS=ON && \
	/usr/local/cmake-3.13.2-Linux-x86_64/bin/cmake --build core-moos-build && \
	/usr/local/cmake-3.13.2-Linux-x86_64/bin/cmake --build core-moos-build --target install && \
	rm -R core-moos-src core-moos-build



ENV PATH="${PATH}:$APP_PATH/cmake-3.13.2-Linux-x86_64/bin"
