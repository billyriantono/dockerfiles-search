FROM planar/mingw-builder:prepare
MAINTAINER Aleksey Yaroslavcev <a.yaroslavcev@gmail.com>

#Make toolchain
USER devel
RUN cd /opt/mxe && \
  make -j`nproc` JOBS=2 openssl glib icu4c freetds MXE_TARGETS=i686-w64-mingw32.shared 