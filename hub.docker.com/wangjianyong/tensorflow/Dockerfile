FROM wangjianyong/jupyter
MAINTAINER Jianyong Wang <wangjianyongscu@gmail.com>
ENV REFRESHED_AT 2016-07-22

#############
# Pick up some TF dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        curl \
        libfreetype6-dev \
        libpng12-dev \
        libzmq3-dev \
        pkg-config \
        python-scipy \
        rsync \
        unzip \
        && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ENV TENSORFLOW_VERSION 0.9.0
# --- DO NOT EDIT OR DELETE BETWEEN THE LINES --- #
# These lines will be edited automatically by parameterized_docker_build.sh. #
# COPY _PIP_FILE_ /
# RUN pip --no-cache-dir install /_PIP_FILE_
# RUN rm -f /_PIP_FILE_

# Install TensorFlow GPU version.
RUN pip --no-cache-dir install \
    http://storage.googleapis.com/tensorflow/linux/gpu/tensorflow-${TENSORFLOW_VERSION}-cp27-none-linux_x86_64.whl
# --- ~ DO NOT EDIT OR DELETE BETWEEN THE LINES --- #

#############
# TensorBoard
EXPOSE 6006
