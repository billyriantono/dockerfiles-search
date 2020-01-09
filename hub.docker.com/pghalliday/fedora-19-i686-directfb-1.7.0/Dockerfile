FROM pghalliday/fedora-19-i686
RUN linux32 yum install -y libX11-devel
RUN linux32 yum install -y libXext-devel
RUN linux32 yum install -y freetype-devel
RUN linux32 yum install -y libjpeg-devel
RUN linux32 yum install -y libpng-devel
RUN linux32 yum install -y zlib-devel
RUN linux32 yum install -y directfb-devel
RUN linux32 yum install -y wget
RUN linux32 yum install -y tar
RUN linux32 wget http://directfb.org/downloads/Core/DirectFB-1.7/DirectFB-1.7.0.tar.gz
RUN linux32 tar zxf DirectFB-1.7.0.tar.gz -C /opt
RUN linux32 yum groupinstall -y "Development Tools"
RUN linux32 yum install -y gcc-c++
WORKDIR /opt/DirectFB-1.7.0
RUN linux32 ./configure
RUN linux32 make
RUN linux32 make install
WORKDIR /
