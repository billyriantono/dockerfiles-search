#
#
#

# Pull base image.
FROM ubuntu:18.04

ARG DEBIAN_FRONTEND=noninteractive

# Install.
RUN \
  apt-get update && \
  apt-get install -y \
    tzdata \
    git \
    doxygen \
    g++ \
    gobjc++ \
    gnustep-devel \
    lcov \
    python3 \
    python3-dev \
    python3-pip \
    ant \
    cmake \
    swig \
    liblog4cxx-dev \
    libdcmtk-dev \
    dcmtk && \
  pip3 install breathe && \
  pip3 install sphinx_rtd_theme && \
  pip3 install dropbox



