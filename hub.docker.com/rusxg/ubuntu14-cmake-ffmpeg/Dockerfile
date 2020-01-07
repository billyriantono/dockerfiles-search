FROM rusxg/ubuntu14-cmake

RUN \
	apt-get update && \
        apt-get -y install libjpeg-dev libpng-dev libtiff-dev \
                autoconf automake libass-dev libfreetype6-dev \
                libtheora-dev libtool libvorbis-dev \
                pkg-config texinfo zlib1g-dev unzip \
                libx264-dev libmp3lame-dev yasm && \
	wget http://ffmpeg.org/releases/ffmpeg-3.2.2.tar.bz2 && \
	tar xvf ffmpeg-3.2.2.tar.bz2 && \
	cd ffmpeg-3.2.2 && \
	./configure --enable-shared --enable-gpl --enable-libx264 --enable-libmp3lame && \
	make && \
	make install && \
	cd .. && rm -rf ffmpeg-3.2.2 && \
        rm ffmpeg-3.2.2.tar.bz2 && \
	apt-get -y clean all && \
	rm -rf /var/lib/apt/lists/*
