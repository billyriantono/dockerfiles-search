FROM tsweb/centos64
MAINTAINER Kazuhisa Kumagai <k-kumagai@ts.tv-osaka.co.jp>

#--------------------------------------
# install FFMpeg 2.1.1
# http://mt.orz.at/archives/2014/01/centos63ffmpeg-1.html
#--------------------------------------

RUN yum install -y vi tar bzip2

RUN yum install -y glibc-devel glibc-headers glibc-static
RUN yum install -y wget
RUN yum install -y patch
RUN yum install -y xz unzip
RUN yum install -y bzip2-devel
RUN yum install -y gcc gcc-c++ make automake libtool
RUN yum install -y fontconfig fontconfig-devel
RUN yum install -y libxml2-devel
RUN yum install -y java-1.6.0-openjdk-devel.x86_64
RUN yum install -y ncurses-devel ncurses-static ncurses-term
RUN yum install -y libpng libpng-devel libpng-static
RUN yum install -y libtiff libtiff-devel libtiff-static
RUN yum install -y lcms lcms-devel lcms-libs
RUN yum install -y git
RUN yum install -y --enablerepo=centosplus openssl-devel
RUN yum install -y libsndfile libsndfile-devel

RUN yum install -y opencv-devel cairo-devel
RUN yum install -y gnutls-devel
RUN yum install -y fftw fftw-devel fftw-static

RUN yum install -y libXtst-devel

ADD ./etc/ld.so.conf.d/ffmpeg.conf /etc/ld.so.conf.d/
ADD ./etc/ld.so.conf.d/local.conf /etc/ld.so.conf.d/
RUN ldconfig

ENV PATH /usr/local/bin:/usr/local/ffmpeg-libs/bin:$PATH
ENV PKG_CONFIG_PATH /usr/local/ffmpeg-libs/lib/pkgconfig

RUN (\
	cd /usr/local/src;\
	wget http://www.cmake.org/files/v2.8/cmake-2.8.11.2.tar.gz;\
	tar -zxvf cmake-2.8.11.2.tar.gz;\
	cd cmake-2.8.11.2;\
	./bootstrap --parallel=4 --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)
ENV CMAKE_ROOT /usr/local/ffmpeg-libs/share/cmake-2.8

RUN (\
	cd /usr/local/src;\
	wget http://www.tortall.net/projects/yasm/releases/yasm-1.2.0.tar.gz;\
	tar -zxvf yasm-1.2.0.tar.gz;\
	cd yasm-1.2.0;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget http://www.nasm.us/pub/nasm/releasebuilds/2.10.09/nasm-2.10.09.tar.xz;\
	tar -Jxvf nasm-2.10.09.tar.xz;\
	cd nasm-2.10.09;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget http://fribidi.org/download/fribidi-0.19.5.tar.bz2;\
	tar -jxvf fribidi-0.19.5.tar.bz2;\
	cd fribidi-0.19.5;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget https://libass.googlecode.com/files/libass-0.10.1.tar.xz;\
	tar -Jxvf libass-0.10.1.tar.xz;\
	cd libass-0.10.1;\
	FRIBIDI_CFLAGS=-I/usr/local/ffmpeg-libs/include PKG_CONFIG_PATH=/usr/local/ffmpeg-libs/lib/pkgconfig ./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget ftp://ftp.videolan.org/pub/videolan/libbluray/0.3.0/libbluray-0.3.0.tar.bz2;\
	tar -jxvf libbluray-0.3.0.tar.bz2;\
	cd libbluray-0.3.0;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

ADD libcaca-0.99.beta18.tar.gz /usr/local/src
RUN (\
	cd /usr/local/src;\
	wget -r http://caca.zoy.org/files/libcaca/libcaca-0.99.beta18.tar.gz;\
	tar -zxvf libcaca-0.99.beta18.tar.gz;\
	cd libcaca-0.99.beta18;\
	./configure --prefix=/usr/local/ffmpeg-libs --disable-java --disable-python;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget http://www.quut.com/gsm/gsm-1.0.13.tar.gz;\
	tar -zxvf gsm-1.0.13.tar.gz;\
	cd gsm-1.0-pl13;\
	sed -i -e "s@^\(INSTALL_ROOT.=\)@\1/usr/local/ffmpeg-libs@" Makefile;\
	sed -i -e "s@^\(GSM_INSTALL_INC.\+\)inc@\1include@" Makefile;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget -O libmodplug-0.8.8.4.tar.gz "http://downloads.sourceforge.net/project/modplug-xmms/libmodplug/0.8.8.4/libmodplug-0.8.8.4.tar.gz?r=http%3A%2F%2Fmodplug-xmms.sourceforge.net%2F&ts=1377681153&use_mirror=jaist";\
	tar -zxvf libmodplug-0.8.8.4.tar.gz;\
	cd libmodplug-0.8.8.4;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget -O lame-3.99.5.tar.gz "http://downloads.sourceforge.net/project/lame/lame/3.99/lame-3.99.5.tar.gz?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Flame%2Ffiles%2Flame%2F3.99%2F&ts=1377682004&use_mirror=jaist";\
	tar -zxvf lame-3.99.5.tar.gz;\
	cd lame-3.99.5;\
	CPPFLAGS="-mfpmath=sse -msse -msse2 -msse3" ./configure --prefix=/usr/local/ffmpeg-libs --enable-nasm;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget -O opencore-amr-0.1.3.tar.gz "http://downloads.sourceforge.net/project/opencore-amr/opencore-amr/opencore-amr-0.1.3.tar.gz?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Fopencore-amr%2Ffiles%2Fopencore-amr%2F&ts=1377682715&use_mirror=jaist";\
	tar -zxvf opencore-amr-0.1.3.tar.gz;\
	cd opencore-amr-0.1.3;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make -j 3;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget https://openjpeg.googlecode.com/files/openjpeg-1.5.1.tar.gz;\
	tar -zxvf openjpeg-1.5.1.tar.gz;\
	cd openjpeg-1.5.1;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget http://downloads.xiph.org/releases/opus/opus-1.0.3.tar.gz;\
	tar -zxvf opus-1.0.3.tar.gz;\
	cd opus-1.0.3;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget http://rtmpdump.mplayerhq.hu/download/rtmpdump-2.4.tar.gz;\
	tar -zxvf rtmpdump-2.4.tar.gz;\
	cd rtmpdump;\
	sed -i -e "s@^\(prefix=/usr/local\)@\1/ffmpeg-libs@" Makefile;\
	sed -i -e "s@^\(prefix=/usr/local\)@\1/ffmpeg-libs@" librtmp/Makefile;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget -O soxr-0.1.1-Source.tar.xz "http://downloads.sourceforge.net/project/soxr/soxr-0.1.1-Source.tar.xz?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Fsoxr%2Ffiles%2F&ts=1377753028&use_mirror=jaist";\
	tar -Jxvf soxr-0.1.1-Source.tar.xz;\
	cd soxr-0.1.1-Source;\
	mkdir build;\
	cd build;\
	cmake -DCMAKE_INSTALL_PREFIX=/usr/local/ffmpeg-libs ..;\
	make;\
	make install;\
)

ADD sdl_x11sym.patch /usr/local/src/
RUN (\
	cd /usr/local/src;\
	wget http://www.libsdl.org/release/SDL-1.2.15.tar.gz;\
	tar -zxvf SDL-1.2.15.tar.gz;\
	cd /usr/local/src/SDL-1.2.15/src/video/x11;\
	cp /usr/local/src/sdl_x11sym.patch .;\
	patch < sdl_x11sym.patch;\
	cd /usr/local/src/SDL-1.2.15;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget http://downloads.xiph.org/releases/ogg/libogg-1.3.1.tar.gz;\
	tar -zxvf libogg-1.3.1.tar.gz;\
	cd libogg-1.3.1;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget http://downloads.xiph.org/releases/speex/speex-1.2rc1.tar.gz;\
	tar -zxvf speex-1.2rc1.tar.gz;\
	cd speex-1.2rc1;\
	./configure --prefix=/usr/local/ffmpeg-libs --enable-sse;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget http://downloads.xiph.org/releases/vorbis/libvorbis-1.3.3.tar.xz;\
	tar -Jxvf libvorbis-1.3.3.tar.xz;\
	cd libvorbis-1.3.3;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget http://downloads.xiph.org/releases/theora/libtheora-1.1.1.tar.bz2;\
	tar -jxvf libtheora-1.1.1.tar.bz2;\
	cd libtheora-1.1.1;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget http://downloads.sourceforge.net/twolame/twolame-0.3.13.tar.gz;\
	tar -zxvf twolame-0.3.13.tar.gz;\
	cd twolame-0.3.13;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	git clone https://github.com/georgmartius/vid.stab.git;\
	cd vid.stab;\
	git checkout release-0.98b;\
	cmake -DCMAKE_INSTALL_PREFIX=/usr/local/ffmpeg-libs .;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget -O vo-aacenc-0.1.3.tar.gz "http://downloads.sourceforge.net/project/opencore-amr/vo-aacenc/vo-aacenc-0.1.3.tar.gz?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Fopencore-amr%2Ffiles%2Fvo-aacenc%2F&ts=1377763066&use_mirror=jaist";\
	tar -zxvf vo-aacenc-0.1.3.tar.gz;\
	cd vo-aacenc-0.1.3;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget -O vo-amrwbenc-0.1.3.tar.gz "http://downloads.sourceforge.net/project/opencore-amr/vo-amrwbenc/vo-amrwbenc-0.1.3.tar.gz?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Fopencore-amr%2Ffiles%2Fvo-amrwbenc%2F&ts=1377763362&use_mirror=jaist";\
	tar -zxvf vo-amrwbenc-0.1.3.tar.gz;\
	cd vo-amrwbenc-0.1.3;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	git clone https://chromium.googlesource.com/webm/libvpx;\
	cd libvpx;\
	git checkout v1.3.0;\
	./configure --prefix=/usr/local/ffmpeg-libs --target=x86_64-linux-gcc;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget http://www.wavpack.com/wavpack-4.60.1.tar.bz2;\
	tar -jxvf wavpack-4.60.1.tar.bz2;\
	cd wavpack-4.60.1;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget ftp://ftp.videolan.org/pub/x264/snapshots/last_x264.tar.bz2;\
	tar -jxvf last_x264.tar.bz2;\
	cd x264-snapshot-*;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	wget http://media.xiph.org/video/derf/y4m/soccer_4cif.y4m;\
	make fprofiled VIDS="soccer_4cif.y4m";\
	make install install-lib-static;\
)

RUN (\
	cd /usr/local/src;\
	wget http://downloads.xvid.org/downloads/xvidcore-1.3.2.tar.gz;\
	tar -zxvf xvidcore-1.3.2.tar.gz;\
	cd xvidcore;\
	cd build/generic/;\
	./bootstrap.sh;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget http://ftp.gnu.org/gnu/libcdio/libcdio-0.90.tar.gz;\
	tar -zxvf libcdio-0.90.tar.gz;\
	cd libcdio-0.90;\
	LDFLAGS=-R/usr/local/ffmpeg-libs/lib ./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget "http://ftp.gnu.org/gnu/libcdio/libcdio-paranoia-10.2+0.90+1.tar.bz2";\
	tar -jxvf libcdio-paranoia-10.2+0.90+1.tar.bz2;\
	cd libcdio-paranoia-10.2+0.90+1;\
	LD_RUN_PATH=/usr/local/ffmpeg-libs/lib CFLAGS=-I/usr/local/ffmpeg-libs/include LDFLAGS=-R/usr/local/ffmpeg-libs/lib ./configure --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget -O gavl-1.4.0.tar.gz "http://downloads.sourceforge.net/project/gmerlin/gavl/1.4.0/gavl-1.4.0.tar.gz?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Fgmerlin%2Ffiles%2Fgavl%2F1.4.0%2F&ts=1428394898&use_mirror=jaist";\
	tar -zxvf gavl-1.4.0.tar.gz;\
	cd gavl-1.4.0;\
	./configure --prefix=/usr/local/ffmpeg-libs --enable-static --with-cpuflags --without-doxygen;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget -O frei0r-plugins-1.3.tar.gz https://files.dyne.org/frei0r/releases/frei0r-plugins-1.3.tar.gz;\
	tar -zxvf frei0r-plugins-1.3.tar.gz;\
	cd frei0r-1.3;\
	./autogen.sh;\
	./configure --prefix=/usr/local/ffmpeg-libs/ --enable-static;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget -O libaacplus-2.0.2.tar.gz http://tipok.org.ua/downloads/media/aacplus/libaacplus/libaacplus-2.0.2.tar.gz;\
	tar -zxvf libaacplus-2.0.2.tar.gz;\
	cd libaacplus-2.0.2;\
	./autogen.sh --prefix=/usr/local/ffmpeg-libs;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget http://mp4v2.googlecode.com/files/mp4v2-2.0.0.tar.bz2;\
	tar -jxvf mp4v2-2.0.0.tar.bz2;\
	cd mp4v2-2.0.0;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make -j 3;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget http://downloads.sourceforge.net/faac/faac-1.28.tar.gz;\
	tar -zxvf faac-1.28.tar.gz;\
	cd faac-1.28;\
	wget http://sources.gentoo.org/cgi-bin/viewvc.cgi/gentoo-x86/media-libs/faac/files/faac-1.28-external-libmp4v2.patch;\
	wget http://sources.gentoo.org/cgi-bin/viewvc.cgi/gentoo-x86/media-libs/faac/files/faac-1.28-libmp4v2_r479_compat.patch;\
	wget http://sources.gentoo.org/cgi-bin/viewvc.cgi/gentoo-x86/media-libs/faac/files/faac-1.28-inttypes.patch;\
	wget http://sources.gentoo.org/cgi-bin/viewvc.cgi/gentoo-x86/media-libs/faac/files/faac-1.28-altivec.patch;\
	patch -p1 < faac-1.28-external-libmp4v2.patch;\
	patch -p0 < faac-1.28-libmp4v2_r479_compat.patch;\
	patch -p0 < faac-1.28-inttypes.patch;\
	patch -p0 < faac-1.28-altivec.patch;\
	./bootstrap;\
	./configure CFLAGS="-I/usr/local/ffmpeg-libs/include -Wno-write-strings" CXXFLAGS="-I/usr/local/ffmpeg-libs/include -Wno-write-strings" --prefix=/usr/local/ffmpeg-libs --enable-drm --with-mp4v2;\
	make;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget http://downloads.sourceforge.net/project/opencore-amr/fdk-aac/fdk-aac-0.1.3.tar.gz;\
	tar -zxvf fdk-aac-0.1.3.tar.gz;\
	cd fdk-aac-0.1.3;\
	./configure --prefix=/usr/local/ffmpeg-libs;\
	make -j 3;\
	make install;\
)

RUN (\
	cd /usr/local/src;\
	wget http://www.ffmpeg.org/releases/ffmpeg-2.1.1.tar.gz;\
	tar -zxvf ffmpeg-2.1.1.tar.gz;\
	cd ffmpeg-2.1.1;\
	sed -i -e "s@^\(#define FF_HUFFMAN_BITS \).*[0-9]*@\112@" libavcodec/huffman.h;\
	sed -i -e "s@vsLocalmotions2TransformsSimple@vsLocalmotions2Transforms@" libavfilter/vf_vidstabtransform.c;\
	./configure --enable-gpl --enable-version3 --enable-nonfree --enable-avisynth --enable-fontconfig --enable-frei0r --enable-gnutls --enable-libaacplus --enable-libass --enable-libbluray --enable-libcaca --enable-libcdio --enable-libfaac --enable-libfdk-aac --enable-libfreetype --enable-libgsm --enable-libmodplug --enable-libmp3lame --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libopenjpeg --enable-libopus --enable-librtmp --enable-libsoxr --enable-libspeex --enable-libtheora --enable-libtwolame --enable-libvidstab --enable-libvo-aacenc --enable-libvo-amrwbenc --enable-libvorbis --enable-libvpx --enable-libwavpack --enable-libx264 --enable-libxvid --disable-outdev=sdl --disable-ffprobe --disable-ffserver --extra-cflags='-I/usr/local/ffmpeg-libs/include' --extra-ldflags='-L/usr/local/ffmpeg-libs/lib -R/usr/local/ffmpeg-libs/lib' --optflags='-O2 -finline-functions';\
	make;\
	make install;\
)

RUN ldconfig

RUN (\
	cd /usr/local/src;\
	wget http://jaist.dl.sourceforge.net/sourceforge/gpac/gpac-0.5.0.tar.gz;\
	tar -zxvf gpac-0.5.0.tar.gz;\
	cd gpac;\
	chmod a+x configure;\
	./configure --prefix=/usr/local;\
	make;\
	make install;\
	ldconfig;\
)
