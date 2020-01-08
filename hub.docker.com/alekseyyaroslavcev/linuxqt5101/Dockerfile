FROM debian:stable
MAINTAINER Aleksey Yaroslavcev <a.yaroslavcev@gmail.com>

COPY qtni5101.qs /

RUN apt-get update

RUN apt-get -y install build-essential

RUN apt-get -y install fakeroot file tree wget curl git lsb rsync

RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash;

RUN apt-get -y install git-lfs;git lfs install

RUN apt-get -y install python

RUN apt-get -y install libudev-dev libusb-1.0-0-dev libgl1-mesa-dev libglib2.0-dev

RUN apt-get -y install libdbus-1-3 libfreetype6 libfontconfig1 libx11-xcb1 libx11-6

RUN apt-get -y clean;apt-get -y autoclean

RUN wget http://master.qt.io/archive/online_installers/3.0/qt-unified-linux-x64-3.0.5-online.run; chmod +x qt-unified-linux-x64-3.0.5-online.run

RUN ./qt-unified-linux-x64-3.0.5-online.run --verbose --platform minimal --script /qtni5101.qs; rm qt-unified-linux-x64-3.0.5-online.run;rm -rf /opt/qt/Docs;rm -rf /opt/qt/Examples;rm -rf /opt/qt/Tools;rm -f /opt/qt/5.10.1/gcc_64/lib/*.debug
