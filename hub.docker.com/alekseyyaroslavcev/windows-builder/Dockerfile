FROM alekseyyaroslavcev/linux-builder-x86
MAINTAINER Aleksey Yaroslavcev <a.yaroslavcev@gmail.com>

#Create devel user...
RUN useradd -m -d /home/devel -u 1000 -U -G users,tty -s /bin/bash devel

#Clone mxe repo
RUN mkdir -p /opt/mxe && \
  git clone https://github.com/mxe/mxe.git /opt/mxe && \
  chown -R devel /opt/mxe && \
  sed -i 's/i686-w64-mingw32_EH   := sjlj dw2/i686-w64-mingw32_EH   := dw2 sjlj/g' /opt/mxe/Makefile
  
#Make toolchain
USER devel
RUN cd /opt/mxe && \
  make -j`nproc` JOBS=2 mingw-w64 gcc openssl glib MXE_TARGETS=i686-w64-mingw32.shared 
