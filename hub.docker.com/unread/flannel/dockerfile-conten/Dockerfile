#
# Python+OpenCV Dockerfile
#
# https://github.com/umeice/opencv
#

# Pull base image.
FROM umeice/python

MAINTAINER @bungoume <bungoume@gmail.com>

# Install OpenCV.
RUN \
  apt-get update && apt-get upgrade -y && \
  pip install numpy && \
  apt-get install -y libjpeg-dev libpng12-dev opencl-headers libeigen3-dev cmake && \
  git clone https://github.com/Itseez/opencv.git && \
  cd opencv && \
  git checkout -b v2.4.9 refs/tags/2.4.9 && \
  cmake . && \
  make && make install

# Define mountable directories.
VOLUME ["/data"]

# Define working directory.
WORKDIR /data

# Define default command.
# CMD ["python"]

# Expose ports.
#   - 5000: HTTP
EXPOSE 5000
