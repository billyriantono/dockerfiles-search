FROM flightgear/plib.build:opensuse-latest AS fgbuild
  
WORKDIR /flightgear

RUN \
  zypper --gpg-auto-import-keys ar http://download.opensuse.org/repositories/KDE:/Qt5/openSUSE_Leap_42.3/KDE:Qt5.repo && \
  zypper --gpg-auto-import-keys in -y \
  libqt5-qtbase-devel \
  libqt5-qtdeclarative-devel \
  libqt5-qtsvg-devel \
  libqt5-linguist-devel \
  libQt5Gui-devel \
  libQt5Widgets-devel

RUN git clone --depth 1 https://git.code.sf.net/p/flightgear/flightgear && \
    mkdir build && cd build && cmake -G "Unix Makefiles" \
                              -D CMAKE_BUILD_TYPE=Release \
                              -D CMAKE_PREFIX_PATH="/usr/local" \
                              -D CMAKE_INSTALL_PREFIX:PATH=/usr/local \
                              -D CMAKE_CXX_FLAGS="-pipe" \
                              ../flightgear \
                        && make && make install
