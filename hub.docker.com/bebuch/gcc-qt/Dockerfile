FROM gcc:8.1

MAINTAINER Benjamin Buch <https://github.com/bebuch-docker>


# install dependencies
RUN apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y \
		cmake python-dev libxml2-dev libxslt-dev \
		libgtest-dev libxcb-xinerama0-dev libssl-dev \
		libxcursor-dev libxcomposite-dev libxdamage-dev \
		libxrandr-dev libdbus-1-dev libfontconfig1-dev \
		libcap-dev libxtst-dev libpulse-dev libudev-dev \
		libpci-dev libnss3-dev libasound2-dev libxss-dev \
		libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev \
		adwaita-icon-theme autopoint bsdmainutils \
		build-essential dconf-gsettings-backend \
		dconf-service debhelper dh-autoreconf \
		dh-strip-nondeterminism firebird-dev \
		firebird3.0-common firebird3.0-common-doc \
		freetds-common freetds-dev gdb gettext \
		gettext-base gir1.2-atk-1.0 gir1.2-atspi-2.0 \
		gir1.2-gst-plugins-base-1.0 gir1.2-gstreamer-1.0 \
		gir1.2-gtk-3.0 gir1.2-pango-1.0 glib-networking \
		glib-networking-common glib-networking-services \
		groff-base gsettings-desktop-schemas intltool-debian \
		iso-codes libarchive-zip-perl libasound2 \
		libasound2-data libasyncns0 libcupsimage2-dev libdconf1 \
		libatk-bridge2.0-0 libatk-bridge2.0-dev \
		libatk1.0-dev libatspi2.0-0 libatspi2.0-dev \
		libbabeltrace-ctf1 libbabeltrace1 libcap2-bin \
		libcolord2 libct4 libcups2-dev libcupsimage2 \
		libdouble-conversion-dev libdouble-conversion1 \
		libdrm-amdgpu1 libdrm-dev libdrm-intel1 \
		libdrm-nouveau2 libdrm-radeon1 libdrm2 libdw1 \
		libegl1-mesa libepoxy-dev libepoxy0 libevdev2 libfbclient2 \
		libfile-stripnondeterminism-perl libflac8 libgbm-dev \
		libgbm1 libgl1-mesa-dev libgl1-mesa-glx libglapi-mesa \
		libgles2-mesa libgles2-mesa-dev libglu1-mesa libglu1-mesa-dev \
		libgraphite2-dev libgstreamer-plugins-base1.0-0 \
		libgstreamer1.0-0 libgtk-3-0 libgtk-3-common \
		libgtk-3-dev libgudev-1.0-0 libib-util \
		libinput-bin libinput-dev libinput10 libjson-glib-1.0-0 \
		libjson-glib-1.0-common libmtdev-dev libmtdev1 libodbc1 \
		libogg0 liborc-0.4-0 libpango1.0-dev libpangoxft-1.0-0 \
		libpciaccess0 libpipeline1 libpopt0 libproxy-dev libproxy1v5 \
		libpulse-mainloop-glib0 libpulse0 libpython3.5 \
		librest-0.7-0 libsndfile1 libsoup-gnome2.4-1 libsoup2.4-1 \
		libsybdb5 libtimedate-perl libtommath1 \
		libvorbis0a libvorbisenc2 libwacom-common \
		libwacom2 libwayland-bin libwayland-client0 libwayland-cursor0 \
		libwayland-dev libwayland-egl1-mesa libwayland-server0 \
		libwrap0 libx11-xcb-dev libx11-xcb1 libxcb-dri2-0 \
		libxcb-dri2-0-dev libxcb-dri3-0 libxcb-dri3-dev libxcb-glx0 \
		libxcb-glx0-dev libxcb-icccm4 libxcb-icccm4-dev libxcb-image0 \
		libxcb-image0-dev libxcb-keysyms1 libxcb-keysyms1-dev \
		libxcb-present-dev libxcb-present0 libxcb-randr0 \
		libxcb-randr0-dev libxcb-render-util0 libxcb-render-util0-dev \
		libxcb-shape0 libxcb-shape0-dev libxcb-sync-dev libxcb-sync1 \
		libxcb-util0 libxcb-xfixes0 libxcb-xfixes0-dev libxcb-xinerama0 \
		libxcb-xkb-dev libxcb-xkb1 libegl1-mesa-dev gperf bison \
		libxfixes-dev libxft-dev libxft2 libxi-dev libxinerama-dev \
		libxkbcommon-dev libxkbcommon-x11-0 libxkbcommon-x11-dev \
		libxkbcommon0 libxshmfence-dev libxshmfence1 \
		libxtst6 libxxf86vm-dev libxxf86vm1 man-db \
		mesa-common-dev odbcinst odbcinst1debian2 pkg-kde-tools \
		po-debconf publicsuffix unixodbc-dev wayland-protocols \
		x11proto-composite-dev x11proto-damage-dev x11proto-dri2-dev \
		x11proto-fixes-dev x11proto-gl-dev x11proto-randr-dev \
		x11proto-record-dev x11proto-xf86vidmode-dev \
		x11proto-xinerama-dev xkb-data libpcre2-dev flex \
	&& apt-get clean


# build Google test
RUN cd /usr/src/gtest \
	&& mkdir build \
	&& cd build \
	&& cmake -DCMAKE_INSTALL_PREFIX=/usr/local /usr/src/gtest \
	&& make \
	&& mv lib*.a /usr/local/lib/ \
	&& cd / \
	&& rm -r /usr/src/gtest/build


# install boost
ENV \
	BOOST_MAJOR=1 \
	BOOST_MINOR=67 \
	BOOST_PATCH=0
ENV \
	BOOST_VERSION=${BOOST_MAJOR}.${BOOST_MINOR}.${BOOST_PATCH} \
	BOOST_DIR=boost_${BOOST_MAJOR}_${BOOST_MINOR}_${BOOST_PATCH} \
	BOOST_ROOT=/opt/boost
RUN cd /opt \
	&& wget "https://dl.bintray.com/boostorg/release/$BOOST_VERSION/source/$BOOST_DIR.tar.bz2" \
	&& tar xvjf $BOOST_DIR.tar.bz2 \
	&& rm $BOOST_DIR.tar.bz2 \
	&& ln -s /opt/$BOOST_DIR /opt/boost
ENV PATH=$PATH:$BOOST_ROOT
RUN cd $BOOST_ROOT \
	&& ./bootstrap.sh \
	&& bjam -j 2 --build-type=complete --layout=versioned stage \
	&& bjam install


# install QT
RUN cd /opt \
	&& git clone https://code.qt.io/qt/qt5.git \
	&& cd qt5 \
	&& git checkout 5.11 \
	&& perl init-repository \
	&& ./configure -opensource -nomake examples -nomake tests -confirm-license -qt-harfbuzz \
	&& make -j2 \
	&& make install \
	&& cd /opt \
	&& rm -rf qt5
ENV Qt5_DIR=/usr/local/Qt-5.11.1
