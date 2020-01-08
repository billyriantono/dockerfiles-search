FROM ubuntu:trusty

RUN rm /bin/sh && ln -s /bin/bash /bin/sh
RUN apt-get -q update && apt-get install -q -y software-properties-common wget
RUN add-apt-repository ppa:brightbox/ruby-ng
RUN apt-get -q update && apt-get install -q -y build-essential git ruby2.3 mesa-common-dev libglu1-mesa-dev libfontconfig1
RUN rm -rf /var/lib/apt/lists/*

WORKDIR /tmp/qt
# no idea how to actually add a file from the repo, so wget it
# there has to be a more sane way of doing this, but this is docker
RUN wget -q https://bitbucket.org/xiannox/trusty-qt5.7-beta-x64/raw/HEAD/qt-installer-noninteractive.qs
RUN wget -q http://download.qt.io/development_releases/qt/5.7/5.7.0-beta/qt-opensource-linux-x64-5.7.0-beta.run
RUN chmod +x qt-opensource-linux-x64-5.7.0-beta.run
RUN ls -la
RUN ./qt-opensource-linux-x64-5.7.0-beta.run --script qt-installer-noninteractive.qs -platform minimal

WORKDIR /
RUN rm -rf /tmp/qt

ENV QT_BASE_DIR=/opt/qt/5.7/gcc_64
ENV QTDIR=$QT_BASE_DIR 
ENV PATH=$QT_BASE_DIR/bin:$PATH 
ENV LD_LIBRARY_PATH=$QT_BASE_DIR/lib/x86_64-linux-gnu:$QT_BASE_DIR/lib:$LD_LIBRARY_PATH 
ENV PKG_CONFIG_PATH=$QT_BASE_DIR/lib/pkgconfig:$PKG_CONFIG_PATH

WORKDIR /usr/

RUN gcc -v
RUN g++ -v
RUN make -v
RUN qmake -v
RUN ruby -v

