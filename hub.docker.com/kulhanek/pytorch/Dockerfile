FROM nvidia/cuda:9.0-base

RUN apt-get update && apt-get install -y \
    git \
    python3 \
    python3-pip \
    python3-dev \
 && rm -rf /var/lib/apt/lists/*

RUN pip3 install torch \
    torchvision \
    opencv-python \
    matplotlib
