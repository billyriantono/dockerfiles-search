FROM alekseyyaroslavcev/mxe-dw2
MAINTAINER Aleksey Yaroslavcev <a.yaroslavcev@gmail.com>

#Make toolchain
USER devel
RUN cd /opt/mxe && \
  make mingw-w64 gcc openssl glib MXE_TARGETS=i686-w64-mingw32.shared 