FROM centos:centos7
MAINTAINER nikaera <gimnikaerast@gmail.com>

ADD centos.repo /etc/yum.repos.d/centos.repo
RUN rpm --import http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-6
RUN rpm -Uhv http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el6.rf.x86_64.rpm

RUN yum -y update

RUN yum -y install glibc gcc gcc-c++ autoconf automake libtool git make nasm pkgconfig; yum clean all
RUN yum -y install SDL-devel a52dec a52dec-devel alsa-lib-devel faac faac-devel faad2 faad2-devel; yum clean all
RUN yum -y install freetype-devel giflib gsm gsm-devel imlib2 imlib2-devel lame lame-devel libICE-devel libSM-devel libX11-devel; yum clean all
RUN yum -y install libXau-devel libXdmcp-devel libXext-devel libXrandr-devel libXrender-devel libXt-devel; yum clean all
RUN yum -y install libogg libvorbis vorbis-tools mesa-libGL-devel mesa-libGLU-devel xorg-x11-proto-devel zlib-devel; yum clean all
RUN yum -y install libtheora theora-tools; yum clean all
RUN yum -y install libjpeg-devel; yum clean all
RUN yum -y install ncurses-devel; yum clean all
RUN yum -y install libdc1394 libdc1394-devel; yum clean all
RUN yum -y install amrnb-devel amrwb-devel opencore-amr-devel; yum clean all
RUN yum -y install wget; yum clean all

WORKDIR /opt
RUN wget https://openjpeg.googlecode.com/files/openjpeg-1.5.1.tar.gz; \
  tar xzf openjpeg-1.5.1.tar.gz; \
  rm openjpeg-1.5.1.tar.gz
RUN cd openjpeg-1.5.1; \
	./configure --prefix="$HOME/ffmpeg_build" --disable-shared; \
	make; \
	make install; \
  rm -rf *

RUN wget http://downloads.xvid.org/downloads/xvidcore-1.3.2.tar.gz; \
  tar xzvf xvidcore-1.3.2.tar.gz; \
  rm -f xvidcore-1.3.2.tar.gz
RUN cd xvidcore/build/generic; \
	./configure --prefix="$HOME/ffmpeg_build"; \
	make; \
	make install; \
  rm -rf *

RUN wget http://downloads.xiph.org/releases/ogg/libogg-1.3.1.tar.gz; \
  tar xzvf libogg-1.3.1.tar.gz; \
  rm -f libogg-1.3.1.tar.gz
RUN cd libogg-1.3.1; \
	./configure --prefix="$HOME/ffmpeg_build" --disable-shared; \
	make; \
	make install; \
  rm -rf *

RUN wget http://downloads.xiph.org/releases/vorbis/libvorbis-1.3.4.tar.gz; \
  tar xzvf libvorbis-1.3.4.tar.gz; \
  rm -f libvorbis-1.3.4.tar.gz
RUN cd libvorbis-1.3.4; \
	./configure --prefix="$HOME/ffmpeg_build" --with-ogg="$HOME/ffmpeg_build" --disable-shared; \
	make; \
	make install; \
  rm -rf *

RUN wget http://downloads.xiph.org/releases/theora/libtheora-1.1.1.tar.gz; \
  tar xzvf libtheora-1.1.1.tar.gz; \
  rm -f libtheora-1.1.1.tar.gz
RUN cd libtheora-1.1.1; \
	./configure --prefix="$HOME/ffmpeg_build" --with-ogg="$HOME/ffmpeg_build" --disable-examples --disable-shared --disable-sdltest --disable-vorbistest; \
	make; \
	make install; \
  rm -rf *

RUN wget http://downloads.sourceforge.net/opencore-amr/vo-aacenc-0.1.2.tar.gz; \
  tar xzvf vo-aacenc-0.1.2.tar.gz; \
  rm -f vo-aacenc-0.1.2.tar.gz
RUN cd vo-aacenc-0.1.2; \
	./configure --prefix="$HOME/ffmpeg_build" --disable-shared; \
	make install; \
  rm -rf *

RUN yum -y remove yasm
RUN wget http://www.tortall.net/projects/yasm/releases/yasm-1.2.0.tar.gz; \
  tar xzfv yasm-1.2.0.tar.gz; \
  rm -f yasm-1.2.0.tar.gz
RUN cd yasm-1.2.0; \
	./configure --prefix="$HOME/ffmpeg_build" --bindir="/usr/local/bin"; \
  make; \
	make install; \
  rm -rf *

RUN git clone http://git.chromium.org/webm/libvpx.git; \
  cd libvpx; \
	./configure --prefix="$HOME/ffmpeg_build" --disable-examples; \
	make; \
	make install; \
  rm -rf *

RUN git clone git://git.videolan.org/x264.git; \
  cd x264; \
	./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin" --enable-static; \
	make install; \
  rm -rf *

RUN export LD_LIBRARY_PATH=/usr/local/lib/:$HOME/ffmpeg_build/lib/; \
	echo /usr/local/lib >> /etc/ld.so.conf.d/custom-libs.conf; \
	echo $HOME/ffmpeg_build/lib/ >> /etc/ld.so.conf.d/custom-libs.conf; \
	ldconfig;

RUN git clone git://source.ffmpeg.org/ffmpeg.git; \
  cd ffmpeg; \
	git checkout release/2.2; \
	PKG_CONFIG_PATH="$HOME/ffmpeg_build/lib/pkgconfig"; \
	export PKG_CONFIG_PATH; \
	./configure --prefix="$HOME/ffmpeg_build" --extra-cflags="-I$HOME/ffmpeg_build/include" --extra-ldflags="-L$HOME/ffmpeg_build/lib" --bindir="/usr/local/bin" \
--extra-libs=-ldl --enable-version3 --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libvpx --enable-libfaac \
--enable-libmp3lame --enable-libtheora --enable-libvorbis --enable-libx264 --enable-libvo-aacenc --enable-libxvid --disable-ffplay \
--enable-libopenjpeg \
--enable-gpl --enable-postproc --enable-nonfree --enable-avfilter --enable-pthreads --arch=x86_64; \
  make install; \
  rm -rf *
