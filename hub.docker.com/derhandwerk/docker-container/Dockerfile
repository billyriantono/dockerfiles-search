FROM ubuntu:artful

# enabling source repositories
RUN sed -i -- 's/#deb-src/deb-src/g' /etc/apt/sources.list && sed -i -- 's/# deb-src/deb-src/g' /etc/apt/sources.list

# fetching package udpates
RUN apt-get update

# installing git
RUN apt-get install git --yes

# Qt build dependencies
RUN apt-get build-dep qt5-default --yes

# X11 dependencies
RUN apt-get install libxcb-xinerama0-dev --yes

# build essentials
RUN apt-get install build-essential perl python git --yes

# libxcb
RUN apt-get install '^libxcb.*-dev' libx11-xcb-dev libglu1-mesa-dev libxrender-dev libxi-dev --yes

# QtWebKit dependencies
RUN apt-get install flex bison gperf libicu-dev libxslt-dev ruby --yes

# QtWebEngine dependencies
RUN apt-get install libssl-dev libxcursor-dev libxcomposite-dev libxdamage-dev libxrandr-dev libdbus-1-dev libfontconfig1-dev libcap-dev libxtst-dev libpulse-dev libudev-dev libpci-dev libnss3-dev libasound2-dev libxss-dev libegl1-mesa-dev gperf bison --yes

# QtMultimedia dependencies
RUN apt-get install libasound2-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev --yes

# cloning qt
RUN git clone git://code.qt.io/qt/qt5.git 

# init repository
RUN cd qt5 && git checkout v5.10.0 && perl init-repository

# configure sources
RUN ./configure -developer-build -opensource -nomake examples -confirm-license -no-gtkstyle

# compile
RUN make -j4

# install
RUN make install

# cleanup
RUN git submodule foreach --recursive "git clean -dfx" && git clean -dfx