##########################################################################################################################################
#   Startup image is the ubuntu based sonarr
##########################################################################################################################################
FROM linuxserver/sonarr

LABEL version="1.0"
LABEL maintainer="laurent.laborde@gmail.com"
LABEL description="Sonarr image offering ffmpegx + mp4 automator"

ENV FFMPEG_RELEASE 4.2.1

WORKDIR /
VOLUME /mp4_automator

##########################################################################################################################################
#   1- Install ffmpeg
#	2- Install PIP
#	3- Install Pythons module necessary to run mo4_automator
#	4- Deploy MP4_Automator in /mp4_automator
##########################################################################################################################################

# Get dependencies for compiling ffmpeg
RUN apt-get update;apt-get -y install build-essential autoconf automake cmake libtool git checkinstall nasm yasm libass-dev libfreetype6-dev libsdl2-dev p11-kit libva-dev libvdpau-dev libvorbis-dev libxcb1-dev libxcb-shm0-dev libxcb-xfixes0-dev pkg-config texinfo wget zlib1g-dev libchromaprint-dev frei0r-plugins-dev gnutls-dev ladspa-sdk libcaca-dev libcdio-paranoia-dev libcodec2-dev libfontconfig1-dev libfreetype6-dev libfribidi-dev libgme-dev libgsm1-dev libjack-dev libmodplug-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libopenjp2-7-dev libopenmpt-dev libopus-dev libpulse-dev librsvg2-dev librubberband-dev librtmp-dev libshine-dev libsmbclient-dev libsnappy-dev libsoxr-dev libspeex-dev libssh-dev libtesseract-dev libtheora-dev libtwolame-dev libv4l-dev libvo-amrwbenc-dev libvorbis-dev libvpx-dev libwavpack-dev libwebp-dev libx264-dev libx265-dev libxvidcore-dev libxml2-dev libzmq3-dev libzvbi-dev liblilv-dev libopenal-dev opencl-dev libjack-dev libbluray-dev libfdk-aac-dev libcunit1 libcunit1-doc libcunit1-dev libavdevice57 libavfilter6 libavresample3 libpostproc54

# Compile AOM
RUN mkdir /ffmpegtemp && cd /ffmpegtemp && mkdir aom && cd /ffmpegtemp/aom && git clone https://aomedia.googlesource.com/aom && cmake aom/ -DBUILD_SHARED_LIBS=1 && make && checkinstall -y --deldoc=yes --pkgversion=1.0.0

# Compile mysofa
RUN cd /ffmpegtemp && git clone https://github.com/hoene/libmysofa && cd /ffmpegtemp/libmysofa/build && cmake .. && cd /ffmpegtemp/libmysofa/build && cpack && dpkg -i *.deb

# Compile ffmpeg
RUN cd /ffmpegtemp && curl -o ffmpeg-${FFMPEG_RELEASE}.tar.bz2 https://ffmpeg.org/releases/ffmpeg-${FFMPEG_RELEASE}.tar.bz2 && tar -xf ffmpeg-${FFMPEG_RELEASE}.tar.bz2 && rm ffmpeg-${FFMPEG_RELEASE}.tar.bz2 && cd ffmpeg-${FFMPEG_RELEASE} && ./configure --enable-gpl --enable-version3 --disable-static --enable-shared --enable-small --enable-avisynth --enable-chromaprint --enable-frei0r --enable-gmp --enable-gnutls --enable-ladspa --enable-libaom --enable-libass --enable-libcaca --enable-libcdio --enable-libcodec2 --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme --enable-libgsm --enable-libjack --enable-libmodplug --enable-libmp3lame --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libopencore-amrwb --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-libpulse --enable-librsvg --enable-librubberband --enable-librtmp --enable-libshine --enable-libsmbclient --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libssh --enable-libtesseract --enable-libtheora --enable-libtwolame --enable-libv4l2 --enable-libvo-amrwbenc --enable-libvorbis --enable-libvpx --enable-libwavpack --enable-libwebp --enable-libx264 --enable-libx265 --enable-libxvid --enable-libxml2 --enable-libzmq --enable-libzvbi --enable-lv2 --enable-libmysofa --enable-openal --enable-opencl --enable-opengl --enable-libdrm --enable-nonfree --enable-libfdk-aac --enable-libbluray && make && apt-get -y purge ffmpeg "libav*" " libpostproc*" ; apt-get -y autoremove && checkinstall -y --deldoc=yes --pkgversion=10:4.2.1 && rm -rf /ffmpegtemp

# Install PIP and modules and mp4 automator
RUN curl -o get-pip.py https://bootstrap.pypa.io/get-pip.py; python get-pip.py; rm get-pip.py; \
    pip install requests;pip install requests[security];pip install requests-cache; \
    pip install babelfish;pip install tmdbsimple;pip install "guessit<2";pip install "subliminal<2"; \
    pip install stevedore==1.19.1;pip install python-dateutil;pip install qtfaststart; \
    curl -o master.zip https://codeload.github.com/mdhiggins/sickbeard_mp4_automator/zip/master  ; unzip master.zip; mv sickbeard_mp4_automator-master mp4_automator_prep; rm master.zip

COPY autoProcess.ini /mp4_automator_prep/
COPY init-mp4-automator.sh /

RUN chmod u+x /init-mp4-automator.sh;chmod -R 777 mp4_automator_prep
ENTRYPOINT ["/init-mp4-automator.sh"]