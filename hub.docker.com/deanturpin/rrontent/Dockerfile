FROM alpine:3.6

RUN apk add --no-cache bash cmake g++ make qt5-qtbase-dev qt5-qtsvg-dev \
&& NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1)