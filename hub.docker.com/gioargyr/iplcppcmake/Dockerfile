###################################
# Dockerfile for c++7 image proce-#
#  ssing in Linux environment     #
# BigDataEurope, Horizon2020      #
#                                 #
# cmake 3.9.4                     #
###################################

FROM gioargyr/imgproclibscpp:1.0.0

MAINTAINER Giorgos Argyriou <gioargyr@gmail.com>

## INSTALLATION OF cmake 3.9.4
RUN wget --directory-prefix=/downloads https://cmake.org/files/v3.9/cmake-3.9.4.tar.gz \
 && cd /downloads \
 && tar -xzvf cmake-3.9.4.tar.gz \
 && cd /downloads/cmake-3.9.4 \
 && ./bootstrap \
 && make -j4 \
 && make install
