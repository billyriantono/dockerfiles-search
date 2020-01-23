FROM debian
MAINTAINER Codie
RUN apt-get update
RUN apt-get --assume-yes install build-essential cmake qtbase5-dev libqt5x11extras5-dev qttools5-dev qttools5-dev-tools libgcrypt20-dev zlib1g-dev libxi-dev libxtst-dev git-core
WORKDIR /opt
RUN git clone https://github.com/keepassx/keepassx.git
WORKDIR /opt/keepassx/build
RUN cmake ..
RUN make
