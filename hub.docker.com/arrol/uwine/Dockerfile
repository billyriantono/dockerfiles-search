FROM ubuntu:bionic

RUN export DEBIAN_FRONTEND noninteractive
RUN dpkg --add-architecture i386
RUN apt-get update
RUN apt-get install -y tar unzip curl xz-utils gnupg2 software-properties-common xvfb
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
RUN curl -s https://dl.winehq.org/wine-builds/winehq.key | apt-key add -
RUN apt-add-repository -y 'deb https://dl.winehq.org/wine-builds/ubuntu/ bionic main'
RUN apt-get install -y wine-staging winetricks
RUN rm -rf /var/lib/apt/lists/*