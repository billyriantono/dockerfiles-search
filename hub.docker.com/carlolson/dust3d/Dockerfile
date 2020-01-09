FROM ubuntu:18.04

ARG CGAL=CGAL-4.13
ARG TAG=1.0.0-beta.23

ENV DEBIAN_FRONTEND noninteractive
ENV CMAKE_BUILD_TYPE release

RUN sed -Ei 's/^# deb-src /deb-src /' /etc/apt/sources.list \
  && apt-get update \
  && apt-get install -y libgl1-mesa-dri libgl1-mesa-glx --no-install-recommends \
  && apt-get install -y --reinstall qtchooser --no-install-recommends \
  && apt-get install -y qtbase5-dev curl cmake \
  && apt-get install -y unzip git qttools5-dev-tools --no-install-recommends \
  && apt-get build-dep -y libcgal-dev --no-install-recommends \
  && apt-mark manual libmpfr6 \
  \
  # INSTALL CGAL
  \
  && cd /opt \
  && curl -Lo $CGAL.zip https://github.com/CGAL/cgal/releases/download/releases/$CGAL/$CGAL.zip \
  && unzip /opt/$CGAL.zip \
  && mkdir /opt/$CGAL/build \
  && cd /opt/$CGAL/build \
  && cmake ../ \
  && make install \
  \
  # INSTALL DUST3D
  \
  && cd /opt \
  && git clone -b $TAG --depth 1 https://github.com/huxingyi/dust3d.git \
  && cd /opt/dust3d \
  && qmake -qt=5 -makefile \
  && make \
  && mv /opt/dust3d/dust3d /usr/bin \
  \
  # CLEAN
  \
  && apt-get purge -y \
    cmake curl git unzip qttools5-dev-tools qtchooser \
    debhelper dpkg-awk ipe \
    gcc '^cpp-.*' '^libperl.*' '^tex.*' \
  && apt-get purge -y `apt-cache pkgnames | grep -v qt | grep -E '^.*-dev$'` \
  && apt-get autoremove -y \
  && rm -rf /opt/* /var/lib/apt/lists/* /var/cache/* /usr/include/*

ENTRYPOINT ["dust3d"]
