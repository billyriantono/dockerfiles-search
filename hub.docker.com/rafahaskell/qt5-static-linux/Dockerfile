FROM ubuntu:18.04

# Metadata indicating an image maintainer.
MAINTAINER <rafa.sa.xp@gmail.com>


# Update the repository sources list
RUN apt-get update

############depois tu me manda uma cópia do teu mirrors ###### BEGIN INSTALLATION ######################
# Devel packages
RUN apt-get install -y build-essential \
    cmake \
    git

# Clean packages installation
RUN apt-get clean

RUN mkdir /Qt
WORKDIR /Qt

# Build Qt
RUN cd /Qt
RUN git clone git://code.qt.io/qt/qt5.git
RUN cd qt5
WORKDIR /Qt/qt5
RUN git checkout 5.5
RUN perl init-repository --no-webkit
RUN ./configure -prefix /Qt/QtStatic -release -opensource -confirm-license -static -no-largefile -no-sql-mysql -no-sql-psql -no-sql-sqlite -no-journald -qt-zlib -no-mtdev -no-gif -qt-freetype -no-openssl -qt-pcre -no-xinput2 -no-glib -no-egl -no-xcursor -no-xfixes -no-xrandr -no-xinerama -no-xinput -qt-xkbcommon-x11 -no-pulseaudio -no-alsa -no-gtkstyle -no-compile-examples -no-nis -no-cups -no-iconv -no-tslib -fontconfig -no-xcb-xlib -no-eglfs -no-directfb -no-linuxfb -no-kms -no-opengl -no-gstreamer -nomake examples -nomake tests -skip qtwebkit -skip qtwebsockets -skip qtwebkit-examples -skip qtwebchannel  -skip qtwebengine -skip qtwayland -skip qtwinextras -skip qtsvg -skip qtsensors -skip qtcanvas3d -skip qtconnectivity -skip declarative -skip multimedia -skip quick1 -no-audio-backend -no-xkbcommon-evdev -no-gui -no-widgets -no-evdev -no-libproxy
RUN make -j4
RUN make install
RUN cd /Qt
RUN rm -rf qt5

##################### INSTALLATION END #####################
