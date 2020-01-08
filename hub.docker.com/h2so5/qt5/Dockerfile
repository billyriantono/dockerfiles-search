FROM ubuntu

RUN sudo apt-get update
RUN sudo apt-get install -y build-essential perl python git
RUN sudo apt-get install -y "^libxcb.*" libx11-xcb-dev libglu1-mesa-dev libxrender-dev libxi-dev
RUN sudo apt-get install -y flex bison gperf libicu-dev libxslt-dev ruby
RUN sudo apt-get install -y libcap-dev libbz2-dev libgcrypt11-dev libpci-dev libnss3-dev build-essential libxcursor-dev libxcomposite-dev libxdamage-dev libxrandr-dev libdrm-dev libfontconfig1-dev libxtst-dev libasound2-dev gperf libcups2-dev libpulse-dev libudev-dev libssl-dev flex bison ruby
RUN sudo apt-get install -y libasound2-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev

RUN git clone git://code.qt.io/qt/qt5.git

WORKDIR qt5
RUN git checkout dev
RUN perl init-repository
RUN ./configure -debug -confirm-license -developer-build -opensource -nomake examples -nomake tests
RUN make -j4
