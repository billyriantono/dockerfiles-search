FROM centos:7
# Download sources
RUN yum -y install wget tar xz unzip freetype fontconfig libX11
WORKDIR /tmp

RUN wget download.qt.io/official_releases/qt/5.13/5.13.1/qt-opensource-linux-x64-5.13.1.run
ADD qt-installer-noninteractive.qs /tmp
RUN chmod +x ./qt-opensource-linux-x64-5.13.1.run
RUN ./qt-opensource-linux-x64-5.13.1.run --script ./qt-installer-noninteractive.qs --platform minimal --verbose
RUN cp /tmp/qt/5.13.1/gcc_64/* /usr/local/ -rf

# Cleanup
RUN rm -rf /tmp/*
