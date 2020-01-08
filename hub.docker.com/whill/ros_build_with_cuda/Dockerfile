FROM whill/ros_build_base:latest

SHELL ["/bin/bash", "-c"]

RUN apt-get update -qq && apt-get install -qq --no-install-recommends \
  wget \
  cmake \
  unzip \
  pkg-config \
  && rm -rf /var/lib/apt/lists/*

RUN cd ~ \
  && mkdir cuda_download \
  && cd cuda_download \
  && wget https://developer.nvidia.com/compute/cuda/10.0/Prod/local_installers/cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64 \
  && dpkg -i cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64 \
  && apt-key add /var/cuda-repo-10-0-local-10.0.130-410.48/7fa2af80.pub \
  && apt-get update -qq \
  && apt-get install -qq --no-install-recommends cuda \
  && rm -f cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64 \
  && rm -rf /var/lib/apt/lists/*
