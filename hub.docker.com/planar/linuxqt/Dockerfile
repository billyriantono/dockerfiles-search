FROM debian:stable
MAINTAINER Aleksey Yaroslavcev <a.yaroslavcev@gmail.com>

COPY qtni.qs /

RUN apt-get update; apt-get -y install build-essential fakeroot file tree wget curl git lsb-base lsb-release rsync python libudev-dev libusb-1.0-0-dev libgl1-mesa-dev libglib2.0-dev libdbus-1-3 libfreetype6 libfontconfig1 libx11-xcb1 libx11-6 libopenblas-dev;apt-get -y clean;apt-get -y autoclean

RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash;

RUN apt-get -y install git-lfs;git lfs install; apt-get -y clean;apt-get -y autoclean

RUN wget http://master.qt.io/archive/qt/5.12/5.12.3/qt-opensource-linux-x64-5.12.3.run; chmod +x qt-opensource-linux-x64-5.12.3.run; ./qt-opensource-linux-x64-5.12.3.run --verbose --platform minimal --script /qtni.qs; rm qt-opensource-linux-x64-5.12.3.run;rm -rf /opt/qt/Docs;rm -rf /opt/qt/Examples;rm -rf /opt/qt/Tools;rm -f /opt/qt/5.12.3/gcc_64/lib/*.debug;rm -f /opt/qt/MaintenanceTool;ls -la /opt/qt/

ENV PATH /opt/qt/5.12.3/gcc_64/bin/:$PATH
