FROM tensorflow/tensorflow:1.8.0-gpu-py3
MAINTAINER bboy.seiok <bboy.seiok@navercorp.com>

USER root

WORKDIR /root

RUN apt-get update
RUN apt-get -y install autoconf automake build-essential git-core libass-dev libgpac-dev libsdl1.2-dev libtheora-dev libtool libvdpau-dev libvorbis-dev libx11-dev libxext-dev libxfixes-dev pkg-config texi2html zlib1g-dev libmp3lame-dev nasm gcc yasm && true
RUN mkdir ~/ffmpeg_sources
RUN cd ~/ffmpeg_sources
RUN git clone --depth 1 git://github.com/mstorsjo/fdk-aac.git
RUN cd fdk-aac
RUN autoreconf -fiv
RUN ./configure --prefix="$HOME/ffmpeg_build" --disable-shared
RUN make
RUN make install
RUN make distclean
RUN cd ~/ffmpeg_sources
RUN wget http://downloads.sourceforge.net/project/lame/lame/3.99/lame-3.99.5.tar.gz
RUN tar xzvf lame-3.99.5.tar.gz
RUN cd lame-3.99.5
RUN ./configure --prefix="$HOME/ffmpeg_build" --enable-nasm --disable-shared
RUN make
RUN make install
RUN make distclean
RUN cd ~/ffmpeg_sources
RUN git clone --depth 1 git://source.ffmpeg.org/ffmpeg
RUN cd ffmpeg
RUN PKG_CONFIG_PATH="$HOME/ffmpeg_build/lib/pkgconfig"
RUN export PKG_CONFIG_PATH
RUN ./configure --prefix="$HOME/ffmpeg_build"--extra-cflags="-I$HOME/ffmpeg_build/include" --extra-ldflags="-L$HOME/ffmpeg_build/lib" --bindir="$HOME/bin" --extra-libs="-ldl" --enable-gpl --enable-libass --enable-libfdk-aac --enable-libmp3lame --enable-nonfree
RUN make
RUN make install
RUN cp ffmpeg /usr/bin/
RUN make distclean
RUN hash -r
RUN ffmpeg 2>&1 | head -n1

