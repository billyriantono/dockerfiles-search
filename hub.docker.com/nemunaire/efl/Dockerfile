FROM debian:stable

# PACKAGES ############################################################

RUN apt-get update && \
    apt-get install -q -y \
    	autoconf \
	automake \
	autopoint \
	build-essential \
	check \
	doxygen \
	gettext \
        git \
	libbullet-dev \
	libcairo-dev \
	libdbus-1-dev \
	libfontconfig1-dev \
	libfreetype6-dev \
	libfribidi-dev \
	libjpeg-dev \
	libgif-dev \
	libgl-dev \
	libgstreamer1.0-dev \
	libgstreamer-plugins-base1.0-dev \
	libmount-dev \
	libpoppler-cpp-dev \
	libpulse-dev \
	libraw-dev \
	librsvg2-dev \
	libsndfile-dev \
	libspectre-dev \
	libssl-dev \
	libtiff-dev \
	libtool \
	libudev-dev \
	libx11-dev \
	libxcomposite-dev \
	libxcursor-dev \
        libxext-dev \
	libxinerama-dev \
	libxrandr-dev \
        libxrender-dev \
	libxtst-dev \
	libxss-dev \
	libz-dev \
	liblua5.2-dev \
	pkg-config \
	python2.7 \
	cython \
	python-dbus-dev \
	python3 \
	cython3 \
	python3-dbus \
	 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


# SOME CONFIGS ########################################################

ENV VERSION=v1.20.4
ENV PYVERSION=v1.20.0
ENV CFLAGS="-O3 -ffast-math -march=native"


# SETUP EFL CORE ######################################################

RUN git clone --depth 1 --branch "${VERSION}" https://git.enlightenment.org/core/efl.git && \
        cd efl && \
	./autogen.sh --prefix=/usr --disable-systemd --with-glib=no --enable-lua-old && \
	make -j$(grep processor /proc/cpuinfo | wc -l) && \
	make install


# SETUP EFL PYTHON BINDINGS ###########################################

RUN git clone --depth 1 --branch "${PYVERSION}" https://git.enlightenment.org/bindings/python/python-efl.git && \
        cd python-efl && \
	make PY=python2.7 build doc install && \
	make PY=python3 build doc install
