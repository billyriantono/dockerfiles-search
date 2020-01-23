# ncview in a container
#
# docker run  --rm \
#        -v /tmp/.X11-unix:/tmp/.X11-unix \
#        -e DISPLAY=unix$DISPLAY \
#        -v $HOME/ncview/.ncviewrc:/home/ncview/.ncviewrc \
#        -v `pwd`:/home/ncview \
# 	 weatherlab/ncview file_to_be_display.nc
#

FROM debian:stretch
LABEL maintainer "Xin Zhang <xin.zhang@langrunweather.com>"

RUN apt-get update && apt-get install -y \
    curl autoconf automake gcc g++ make libnetcdf-dev libhdf5-dev libexpat1-dev libudunits2-dev  xserver-xorg-dev libxaw7-dev \
    --no-install-recommends \
    && rm -rf /var/lib/apt/lists/* 

RUN curl -O ftp://cirrus.ucsd.edu/pub/ncview/ncview-2.1.7.tar.gz \
    && tar xvf ncview-2.1.7.tar.gz \
    && rm -f ncview-2.1.7.tar.gz \
    && cd ncview-2.1.7 \
    && ./configure CC=/usr/bin/cc \
    && make \
    && make install \
    && cd .. \
    && rm -fr ncview-2.1.7

ENV HOME /home/ncview
RUN useradd --create-home --home-dir $HOME ncview \
	&& chown -R ncview:ncview $HOME

WORKDIR $HOME
USER ncview

ENTRYPOINT [ "ncview" ]
