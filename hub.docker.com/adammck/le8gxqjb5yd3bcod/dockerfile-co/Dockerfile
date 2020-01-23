FROM ubuntu:18.04
LABEL maintainer "Adam Bozson <adam@bozson.io>"

RUN apt-get update && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    --no-install-recommends

WORKDIR /tmp
RUN apt-get -y install module-init-tools libglvnd-dev wget \
    && wget http://uk.download.nvidia.com/XFree86/Linux-x86_64/435.21/NVIDIA-Linux-x86_64-435.21.run \
    && chmod u+x NVIDIA-Linux-x86_64-435.21.run \
    && ./NVIDIA-Linux-x86_64-435.21.run -a --ui=none --no-kernel-module --no-questions

RUN apt-get install -y mesa-utils

CMD ["glxgears"]

