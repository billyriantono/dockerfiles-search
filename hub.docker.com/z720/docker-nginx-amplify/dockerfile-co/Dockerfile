# tomas789/kitti2bag
FROM ros:lunar-ros-base

RUN apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get -y install \
    ros-lunar-cv-bridge \
    ros-lunar-opencv3 \
    ros-lunar-tf \
    python-pip python-matplotlib \
  && rm -rf /var/lib/apt/lists/*
COPY . /kitti2bag
RUN pip install --upgrade pip
RUN pip install numpy==1.12
RUN pip install -e /kitti2bag

WORKDIR /data

ENTRYPOINT ["/kitti2bag/docker_entrypoint.sh"]
