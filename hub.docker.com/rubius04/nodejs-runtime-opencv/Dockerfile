FROM google/nodejs
MAINTAINER Evgeny Timoshenko <evgeny.timoshenko@rubius.com>

RUN apt-get update -y && \
    apt-get install --no-install-recommends -y -q \
        build-essential cmake wget unzip

RUN wget https://github.com/Itseez/opencv/archive/2.4.11.zip
RUN unzip 2.4.11.zip
RUN cd opencv-2.4.11 && cmake . && make -j 8 && make install
RUN rm -rf opencv-2.4.11
