FROM bvlc/caffe:gpu

MAINTAINER Ivona Tautkute "ivona.tautkute@tooploox.com"

ARG KERAS_VERSION=2.1.6
ARG TF_VERSION=1.6

RUN pip install jupyterlab
RUN pip install sklearn
RUN pip install opencv-python

RUN pip install tensorflow==${TF_VERSION} --upgrade
RUN pip install keras==${KERAS_VERSION} --upgrade