# -*- mode: dockerfile -*-
# dockerfile to build libmxnet.so on GPU
FROM tensorflow/tensorflow:latest-gpu


COPY install/tfDlib.sh install/
RUN chmod +x install/tfDlib.sh
RUN install/tfDlib.sh
