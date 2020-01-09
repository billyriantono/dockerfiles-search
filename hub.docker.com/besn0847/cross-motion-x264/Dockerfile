FROM ubuntu:trusty

RUN apt-get update && \
        apt-get install -y --force-yes --no-install-recommends \
                vim build-essential cmake git-core pkg-config wget autoconf automake build-essential pkgconf libtool libzip-dev libjpeg-dev && \ 
        apt-get autoclean && \
        apt-get autoremove && \
        rm -rf /var/lib/apt/lists/*


RUN mkdir /sandbox && \
	cd /sandbox && \
	git config --global http.sslVerify false && \
	git clone https://github.com/raspberrypi/tools.git /opt/tools && \
	git clone https://github.com/Mr-Dave/motion.git &&\
	git clone https://github.com/raspberrypi/userland.git &&\
	wget http://www.ijg.org/files/jpegsrc.v9.tar.gz && \
	tar xvfz jpegsrc.v9.tar.gz && \
	rm -rf jpegsrc.v9.tar.gz && \
	git clone -b release/3.3 git://source.ffmpeg.org/ffmpeg.git && \
	cd ffmpeg && \
	git clone git://git.videolan.org/x264

ENV CCPREFIX "/opt/tools/arm-bcm2708/arm-rpi-4.9.3-linux-gnueabihf/bin/arm-linux-gnueabihf-"
ENV CC "/opt/tools/arm-bcm2708/arm-rpi-4.9.3-linux-gnueabihf/bin/arm-linux-gnueabihf-gcc"
ENV LDFLAGS "-L/opt/arm/lib"
ENV CFLAGS "-I/opt/arm/include"

RUN cd /sandbox/jpeg-9/ && \
	./configure --host=arm-unknown-linux-gnueabi --prefix=/opt/arm && \
	make && \
	make install

RUN cd /sandbox/ffmpeg/x264 && \
	./configure --host=arm-unknown-linux-gnueabi --enable-static --cross-prefix=${CCPREFIX} --prefix=/opt/arm --extra-cflags='-march=armv6' --extra-ldflags='-march=armv6' && \
	make && \
	make install

RUN cd /sandbox/ffmpeg && \
	pkg_config=$(which pkg-config) PKG_CONFIG_PATH=/opt/arm/lib/pkgconfig ./configure --enable-cross-compile --cross-prefix=${CCPREFIX} --arch=armel --target-os=linux --prefix=/opt/arm --enable-gpl --enable-libx264 --enable-nonfree --extra-cflags="-I/opt/arm/include" --extra-ldflags="-L/opt/arm/lib" --extra-libs=-ldl && \
	make && \
	make install

ENV CMAKE_C_COMPILER "/opt/tools/arm-bcm2708/arm-rpi-4.9.3-linux-gnueabihf/bin/arm-linux-gnueabihf-gcc"
ENV CMAKE_CXX_COMPILER "/opt/tools/arm-bcm2708/arm-rpi-4.9.3-linux-gnueabihf/bin/arm-linux-gnueabihf-g++"
ENV MMAL_CFLAGS="-I/opt/vc/include"
ENV MMAL_LIBS="-L/opt/vc/lib"

RUN cd /sandbox/userland && \
	export PATH=$PATH:/opt/tools/arm-bcm2708/arm-rpi-4.9.3-linux-gnueabihf/bin/ && \
	./buildme /

ADD ./configure.ac /sandbox/motion/

RUN cd /sandbox/motion && \
	autoreconf -fiv && \
	./configure --with-ffmpeg=/opt/arm/  --host=arm-unknown-linux-gnueabi --prefix=/opt/arm  --without-sqlite3 && \
	make && \
	make install

RUN cd / && \
	tar cvf /arm-motion-x264.tar /opt/arm/ /opt/vc/ && \
	bzip2 /arm-motion-x264.tar
