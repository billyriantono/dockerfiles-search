FROM ubuntu:15.04 
RUN apt-get update
RUN apt-get install -y \
    autoconf automake autopoint bash bison bzip2 cmake flex \
    gettext git g++ gperf intltool libffi-dev libtool \
    libltdl-dev libssl-dev libxml-parser-perl make openssl \
    p7zip-full patch perl pkg-config python ruby scons sed \
    unzip wget xz-utils libtool-bin g++-multilib libc6-dev-i386
RUN git clone https://github.com/mxe/mxe.git ; \
    cd mxe ; \
    make MXE_TARGETS='x86_64-w64-mingw32.static' gcc qt5 cmake sdl2 make