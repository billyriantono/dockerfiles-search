## https://github.com/openthread/openthread.git
FROM alpine:latest

RUN apk add --no-cache cmake g++ git autoconf automake libtool make linux-headers

RUN git clone https://github.com/openthread/openthread.git

WORKDIR openthread

RUN ./bootstrap \
	&& ./configure

RUN make distclean \
	&& make -f examples/Makefile-posix

#RUN cmake  -DCMAKE_BUILD_TYPE=Debug ../examples && make

#EXPOSE 5683/udp 5684/udp 5685/udp
