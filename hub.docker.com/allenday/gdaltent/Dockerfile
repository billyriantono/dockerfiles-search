FROM            buildpack-deps:jessie
MAINTAINER      Allan Lei <allanlei@helveticode.com>

ADD             src/ /usr/src/
WORKDIR         /usr/src/protobuf
RUN             ln -s /usr/src/googletest gtest
RUN             ./autogen.sh && \
                ./configure && \
                make && \
                make check && \
                make install && \
                ldconfig
