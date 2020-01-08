FROM alpine:latest

RUN apk add --no-cache cmake g++ git autoconf automake libtool make 
RUN git clone https://github.com/eclipse/wakaama.git

WORKDIR /wakaama/build
RUN cmake  -DCMAKE_BUILD_TYPE=Debug ../examples && make

EXPOSE 5683/udp 5684/udp 5685/udp
