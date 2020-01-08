FROM congying/ubuntu-dev:14.04

MAINTAINER Congying <congying1112@gmail.com>

RUN apt-get install -y git
RUN cd /tmp && git clone https://github.com/qt/qt5.git

RUN cd /tmp/qt5 && git checkout 5.3.2
RUN cd /tmp/qt5 && ./init-repository
RUN cd /tmp/qt5 && ./configure -prefix $PWD/qtbase -opensource -nomake tests && make -j4
RUN cd /tmp/qt5 && make install

RUN apt-get remove git
RUN rm -rf /tmp/*