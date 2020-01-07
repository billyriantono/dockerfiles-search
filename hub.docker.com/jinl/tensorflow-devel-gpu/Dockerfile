FROM tensorflow/tensorflow:1.4.0-rc0-devel-gpu
MAINTAINER Jin Li <jinlmsft@live.com>

RUN apt-get -y update && \
    apt-get -y install \
      openssh-server sudo screen python-numpy python-dev python-pip python-wheel libcupti-dev 

WORKDIR /tensorflow

# RUN sed -i -e 's/00fb4a83a4dd1c046b19730a80e2183acc647715b7a8dcc8e808d49ea5530ca8/a8da6d42ac7419e543a27e405f8b660f7b065e9ba981cc9cdcdcecb81af9cc43/g' /tensorflow/tensorflow/workspace.bzl
# RUN sed -i '\@https://github.com/google/protobuf/archive/0b059a3d8a8f8aa40dde7bea55edca4ec5dfea66.tar.gz@d' /tensorflow/tensorflow/workspace.bzl
# RUN bazel clean
