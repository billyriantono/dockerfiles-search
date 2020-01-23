# FSV: File System Visualizer
#
# Original: http://fsv.sourceforge.net/
# GTK2 port: http://fedorchenko.net/fsv2.php
#
# To run:
#
#   docker run \
#     -v /tmp/.X11-unix:/tmp/.X11-unix \
#     -v /dev/dri:/dev/dri:rw \
#     --privileged=true \
#     -e DISPLAY=$DISPLAY \
#     -v $HOME:/data:ro \
#     andrewseidl/fsv2
#
# fsv2 will visualize `/data` by default. Remove the dri and
# privileged lines to disable hardware acceleration.

FROM debian:jessie
MAINTAINER Andrew Seidl <dev@aas.io>

RUN apt-get update && apt-get install -y \
    curl \
    build-essential \
    libftgl-dev \
    libgl1-mesa-dri \
    libgtkgl2.0-dev \
    libgtkmm-2.4-dev \
    --no-install-recommends

RUN cd /usr/src && \
    curl -O http://fedorchenko.net/src/fsv2-1.1.0.tar.bz2 && \
    tar jxvf fsv2-1.1.0.tar.bz2 && \
    cd fsv2-1.1.0 && \
    ./configure && \
    make

WORKDIR /data
 
ENTRYPOINT [ "/usr/src/fsv2-1.1.0/src/fsv2" ]
